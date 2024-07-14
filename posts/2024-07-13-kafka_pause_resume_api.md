<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="../assets/css/style.css">
</head>
<body>
<header>
    <h1>kafka pause/resume api</h1>
    <p>Posted on 2024-07-13</p>
</header>
<main>
<p>kafka 를 운영할때 컨슘행위를 잠시 중단해야할 필요가 있을수도 있다.</p>
<p>예를들어 여러 토픽에 대한 메시지 발행이 한번에 너무 많이 몰려 우선순위가 낮은 토픽을 잠시 중지시켜놓는 경우가 있을수 있다.&nbsp;</p>
<p>&nbsp;</p>
<p>이때 Kafka 라이브러리에서 제공하는 pause/resume 기능을 통해 일시적으로 중단했다가 재개 할수 있다.&nbsp;</p>
<p>예를들어 다음과 같이 컨슈머가 구성되어 있을때를 예를들어보자.&nbsp;</p>
<p>&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/lOjnp/btsIxEVbqn6/wIqxIGZK7M6cyZG0uckhy1/img.png" /></span><figcaption>메시지는 현재 5번까지 소비(consume)되었고, 아직 소비되지 않은 메시지 6,7,8을 pause 하고 싶을때.</figcaption>
</figure>
</p>
<p>&nbsp;</p>
<p>이때 pause를 하게 되면 처리된 오프셋 5번까지의 정보는 저장되고, resume 하는 시점에 6,7,8을 다시 컨슈머가 처리하게 된다.&nbsp;</p>
<p>&nbsp;</p>
<p>Pause를 호출할 경우 아래와 같이 된다. (P 라고 표시된 메시지 하나가 현재 떠있는 모든 파드에 pause를 시키게 된다. )</p>
<p>&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/4tfVt/btsIyuj92RQ/BKNjUtzxcMhMco5LDbJfzk/img.png" /></span><figcaption>pause 호출시 처리과정</figcaption>
</figure>
</p>
<p>&nbsp;</p>
<p>여기서 의문점이 생길수 있다.</p>
<blockquote><span style="font-family: 'Noto Serif KR';">각 파티션은 기본적으로 컨슈머 하나에 연결되는데, 어떻게 하나의 메시지가 모든 파드에 pause 시킬수 있지?&nbsp;</span><br /><br /></blockquote>
<p>카프카의 각 파티션이 하나의 컨슈머와 묶이는 원리는 "<b>컨슈머 그룹</b>" 이라는 개념 때문이다.&nbsp;</p>
<p>Kafka 컨슈머 리스너는 위와 같이 파티션별 메시지의 중복처리가 되지 않도록 하기 위해 컨슈머 그룹을 설정하고, 그 그룹별로 토픽을 구독 하여 소비(consume) 하도록 처리하기 때문에 메시지의 중복처리가 되지 않는다. 아래와 같다.&nbsp;</p>
<p>&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/kKB0Z/btsIy5qsNvP/KfrUPkooKMqAkNv9AKQqCk/img.png" /></span><figcaption>kafka는 일반적으로 업무영역별 컨슈머 그룹을 설정하고, 토픽을 구독하여 소비(consume) 하는 방식이다.</figcaption>
</figure>
</p>
<p>&nbsp;</p>
<p>다시 본론으로 돌아가서 pause 를 호출한다고 했을때 컨슈머 그룹을 다르게 설정하면 다음과 같이 된다.&nbsp;</p>
<p>&nbsp;</p>
<p><figure class="imageblock alignCenter"><span><img src="https://blog.kakaocdn.net/dn/bATcv9/btsIzMjDjOV/GFBoQfOYUbpWM9o1KUpm6K/img.png" /></span><figcaption>이 내용이 pause/resume 기능의 핵심이다. 컨슈머 그룹이 달라지게 되기 때문에 모든 파드에서 pause/resume 메시지를 소비해야한다.</figcaption>
</figure>
</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<hr contenteditable="false" />
<p>코드를 구현해보면 다음과 같다.&nbsp;</p>
<h2>Controller (pause 메시지의 발행 관련 영역)&nbsp;</h2>
<pre class="java" id="code_1720928909273"><code>@RestController
KafkaPauseResumeController {

	// kafka message produce 하기 위한 서비스 클래스 
	private final KafkaListenerService kafkaListenerService kafkaListenerService;     
    
    // pause 구현 
    @PutMapping // 결과가 달라지지 않기 때문에 Put 메서드 
    public void pauseListener(@PathVariable("id") String listenerId) { // listenerId = topic 
    	if(StringUtils.isBlank(listenerId)) {
        	throw new IllegalArgumentException("listener id is essential"); 
        }
        
        kafkaListenerService.produceMessage(listenerId, "pause"); 
    }

	// resume 구현 
    @PutMapping // 결과가 달라지지 않기 때문에 Put 메서드 
    public void resumeListener(@PathVariable("id") String listenerId) { // listenerId = topic 
    	if(StringUtils.isBlank(listenerId)) {
        	throw new IllegalArgumentException("listener id is essential"); 
        }
        
        kafkaListenerService.produceMessage(listenerId, "resume"); 
    }
}


KafkaListenerService {

	private final JsonProducer jsonProducer; 
    
	public void produceMessage(String listnerId, String action) {
    	jsonProducer.sendMessageAsync(KafkaConst.Topic.토픽명, listenerId, action); 
    }

}


// Json Producer는 아래와 같이 구성했다. 
// 필수적인 코드만 기재하고 나머지는 생략 
JsonProducer {
    private final KafkaTemplate&lt;String, Object&gt; jsonKafkaTemplate;

	public void sendMessageAsync(String topic, String key, Object msg) {
    	ProducerRecord&lt;String, Object&gt; record = new ProducerRecord&lt;&gt;(topic, null, System.currentTimeMillis(), key, msg); 
        ListenableFuture&lt;SendResult&lt;String, Object&gt;&gt; future = jsonKafkaTemplate.send(record);
        
        // callback 구현 필요시 처리 
        // 통상적으로 실패건에 대해서만 구현한다. 
        future.addCallback(new ListenableFutureCallback&lt;&gt;() {
        
            @Override 
            public void onFailure(Throwable throwable) {
                log.error("error message / topic : {}, key : {}", topic, key); 
            }
        }
    }
}</code></pre>
<p>&nbsp;</p>
<h2>Consumer (발행한 메시지의 소비)&nbsp;</h2>
<pre class="java" id="code_1720929573716"><code>KafkaListenerConsumer {
	private final KafkaListenerService kafkaListenerService; 
    
    @KafkaListener(topics = "토픽명(여기서는 A 라하겠음", 
    			   // random한 uuid를 생성하는 방식으로 각 컨슈머의 컨슈머 그룹을 다르게 만든다. 
                   // 이렇게 해야 A 토픽이 관련 각 파드 리스너가 다른 컨슈머 그룹에 속해서 
                   // 하나의 메시지에 대해 모두 소비할수 있음 
                   groupId = "컨슈머그룹"+"-"+"#{T(java.util.UUID).randomUUID().toString()}", 
                   containerFactory = "jsonKafkaListenerContainerFactory" // 카프카 리스너 설정                                          						
    )
    public void operate(ConsumerRecord&lt;String, String&gt; record, ConsumerRecordMetadata meta) {
    	if("pause") 
        	kafkaListenerService.pauseListener(key); 
        else if("resume") 
        	kafkaListenerService.resumeListener(key); 
        
    }
	
}</code></pre>
</main>
</body>
</html>