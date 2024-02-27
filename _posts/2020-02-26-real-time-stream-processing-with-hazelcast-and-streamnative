---
layout: post
title: Real-Time Stream Processing With Hazelcast and StreamNative
subtitle: In this article, readers will learn about real-time stream processing with Hazelcast and StreamNative in a shorter time, along with demonstrations and code.
cover-img: /assets/img/path.jpg
thumbnail-img: /assets/img/thumb.png
share-img: /assets/img/path.jpg
tags: [ml, streamprocessing]
author: Fawaz Ghali and Tim Spann
---

<p>One of the most useful features of real-time stream processing is to combine the strengths and advantages of various technologies to provide a unique developer experience and an efficient way of processing data in real-time at scale. Hazelcast is a real-time distributed computation and storage platform for consistently low latency queries, aggregation, and stateful computation against real-time event streams and traditional data sources. Apache Pulsar is a real-time multitenant geo-replicated distributed pub-sub messaging and streaming platform for real-time workloads, handling millions of events per hour.&nbsp;</p>
<p>However, real-time stream processing is not an easy task, especially when combining multiple live streams with large volumes of data stored in external data storages to provide context and instant results. When it comes to usage, Hazelcast can be used for the following things:</p>
<ul>
    <li dir="ltr">Stateful data processing over real-time streaming data.</li>
    <li dir="ltr">Data at rest.</li>
    <li dir="ltr">A combination of data at rest and stateful data processing over real-time streaming data.&nbsp;</li>
    <li dir="ltr">Querying streaming.</li>
    <li dir="ltr">Batch data sources directly using SQL.</li>
    <li dir="ltr">Distributed coordination for microservices.</li>
    <li dir="ltr">Replicating data from one region to another.&nbsp;</li>
    <li dir="ltr">Replicating data between data centers in the same region.</li>
</ul>
<p dir="ltr">While Apache Pulsar can be used for messaging and streaming, use cases take the place of multiple products and provide a superset of their features. Apache Pulsar is a cloud-native multitenant unified messaging platform to replace Apache Kafka, RabbitMQ, MQTT, and legacy messaging platforms. Apache Pulsar provides an infinite message bus for Hazelcast to act as an instant source and sink for any and all data sources.</p>
<p dir="ltr"><img style="width: 550px;" class="fr-fic fr-dib ls-is-cached lazyloaded" data-image="true" data-new="false" data-sizeformatted="55.8 kB" data-mimetype="image/jpeg" data-creationdate="1674834823611" data-creationdateformatted="01/27/2023 03:53 PM" data-type="temp" data-url="https://dz2cdn1.dzone.com/storage/temp/16670841-7de2a147-003d-4ba7-a7ce-e6023d47997b.jpeg" data-modificationdate="null" data-size="55839" data-name="7de2a147-003d-4ba7-a7ce-e6023d47997b.jpeg" data-id="16670841" data-src="https://dz2cdn1.dzone.com/storage/temp/16670841-7de2a147-003d-4ba7-a7ce-e6023d47997b.jpeg" alt="The Hazelcast Platform" src="https://dz2cdn1.dzone.com/storage/temp/16670841-7de2a147-003d-4ba7-a7ce-e6023d47997b.jpeg"></p>
<h2 dir="ltr">Prerequisites</h2>
<p><span data-preserver-spaces="true">We&rsquo;re building an application where we ingest data from Apache Pulsar into Hazelcast and then process it in real time. To run this application, make sure your system has the following components:</span></p>
<ul>
    <li><span data-preserver-spaces="true">Hazelcast installed on your system: we&rsquo;re using CLI.</span></li>
    <li><span data-preserver-spaces="true">Pulsar installed on your system: we&rsquo;re using Docker.</span></li>
</ul>
<p><span data-preserver-spaces="true">If you have macOS and Homebrew, you can install Hazelcast using the following command:</span></p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Shell</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="brew tap hazelcast/hz

brew install hazelcast@5.2.1" data-lang="text/x-sh"><pre><code lang="text/x-sh">brew tap hazelcast/hz

brew install hazelcast@5.2.1</code></pre></div></div></div>
<p>
    <br>
</p>
<p dir="ltr">&nbsp;Check if Hazelcast is installed:</p>
<p dir="ltr"><code>hz -V</code></p>
<p dir="ltr">&nbsp;Then start a local cluster:</p>
<p dir="ltr"><code>hz start</code>&nbsp;</p>
<p dir="ltr">You should see the following in the console:</p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Shell</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="INFO: [192.168.1.164]:5701 [dev] [5.2.1]

 

Members {size:1, ver:1} [

     Member [192.168.1.164]:5701 - 4221d540-e34e-4ff2-8ad3-41e060b895ce this

]" data-lang="text/x-sh"><pre><code lang="text/x-sh">INFO: [192.168.1.164]:5701 [dev] [5.2.1]

 

Members {size:1, ver:1} [

     Member [192.168.1.164]:5701 - 4221d540-e34e-4ff2-8ad3-41e060b895ce this

]</code></pre></div></div></div>
<p dir="ltr">
    <br>
</p>
<p dir="ltr">You can start Pulsar in Docker using the following command:&nbsp;</p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Shell</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="docker run -it -p 6650:6650 -p 8080:8080 \

    --mount source=pulsardata,target=/pulsar/data \

    --mount source=pulsarconf,target=/pulsar/conf \

    apachepulsar/pulsar:2.11.0 bin/pulsar standalone" data-lang="text/x-sh"><pre><code lang="text/x-sh">docker run -it -p 6650:6650 -p 8080:8080 \

    --mount source=pulsardata,target=/pulsar/data \

    --mount source=pulsarconf,target=/pulsar/conf \

    apachepulsar/pulsar:2.11.0 bin/pulsar standalone</code></pre></div></div></div>
<p>
    <br>
</p>
<p dir="ltr">To install Management Center, use one of the following methods, depending on your operating system:</p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Shell</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="brew tap hazelcast/hz

brew install hazelcast-management-center@5.2.1" data-lang="text/x-sh"><pre><code lang="text/x-sh">brew tap hazelcast/hz

brew install hazelcast-management-center@5.2.1</code></pre></div></div></div>
<p>
    <br>
</p>
<p dir="ltr">Check that Management Center is installed:</p>
<p dir="ltr"><code>hz-mc -V</code></p>
<h2 dir="ltr">Data Collection</h2>
<p dir="ltr"><img style="width: 550px;" class="fr-fic fr-dib ls-is-cached lazyloaded" data-image="true" data-new="false" data-sizeformatted="16.9 kB" data-mimetype="image/png" data-creationdate="1674834889965" data-creationdateformatted="01/27/2023 03:54 PM" data-type="temp" data-url="https://dz2cdn1.dzone.com/storage/temp/16670843-86e4ea3a-cefc-477a-bf1b-66c644a3cee5.png" data-modificationdate="null" data-size="16927" data-name="86e4ea3a-cefc-477a-bf1b-66c644a3cee5.png" data-id="16670843" alt="Data Collection" data-src="https://dz2cdn1.dzone.com/storage/temp/16670843-86e4ea3a-cefc-477a-bf1b-66c644a3cee5.png" src="https://dz2cdn1.dzone.com/storage/temp/16670843-86e4ea3a-cefc-477a-bf1b-66c644a3cee5.png"></p>
<p><span data-preserver-spaces="true">For our application, we wish to ingest air quality readings from around the United States via the AirNow data provider.&nbsp;</span></p>
<p><em>Source</em><span data-preserver-spaces="true">:&nbsp;</span><a href="https://docs.airnowapi.org/" target="_blank">AirNow API</a></p>
<p><span data-preserver-spaces="true">With a simple Java application, we make REST calls to the AirNow API that provides air quality reading for major zip codes around the United States. The Java application sends the JSON-encoded AirNow data to the &ldquo;airquality&rdquo; Pulsar topic. From this point, a Hazelcast application can read it.&nbsp;</span></p>
<p><em>Source</em><span data-preserver-spaces="true">:&nbsp;</span><a href="https://github.com/tspannhw/spring-pulsar-airquality" target="_blank">GitHub</a></p>
<p><span data-preserver-spaces="true">We also have a Java Pulsar function receiving each event from the &ldquo;airquality&rdquo; topic and parsing it into different topics based on which type of air quality reading it is. This includes PM2.5, PM10, and Ozone.</span></p>
<p dir="ltr"><em>Source</em>: <a href="https://github.com/tspannhw/pulsar-airquality-function" rel="noopener noreferrer" target="_blank">GitHub</a>&nbsp;</p>
<h3 dir="ltr">Example AirQuality Data</h3>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">JSON</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code='{"dateObserved":"2023-01-19 ","hourObserved":12,"localTimeZone":"EST","reportingArea":"Philadelphia","stateCode":"PA","latitude":39.95,"longitude":-75.151,"parameterName":"PM10","aqi":19,"category":{"number":1,"name":"Good","additionalProperties":{}},"additionalProperties":{}}' data-lang="application/json"><pre><code lang="application/json">{&quot;dateObserved&quot;:&quot;2023-01-19 &quot;,&quot;hourObserved&quot;:12,&quot;localTimeZone&quot;:&quot;EST&quot;,&quot;reportingArea&quot;:&quot;Philadelphia&quot;,&quot;stateCode&quot;:&quot;PA&quot;,&quot;latitude&quot;:39.95,&quot;longitude&quot;:-75.151,&quot;parameterName&quot;:&quot;PM10&quot;,&quot;aqi&quot;:19,&quot;category&quot;:{&quot;number&quot;:1,&quot;name&quot;:&quot;Good&quot;,&quot;additionalProperties&quot;:{}},&quot;additionalProperties&quot;:{}}</code></pre></div></div></div>
<p dir="ltr">
    <br>
</p>
<h3 dir="ltr">Example Ozone Data</h3>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">JSON</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code='{"dateObserved":"2023-01-19 ","hourObserved":12,"localTimeZone":"EST","reportingArea":"Philadelphia","stateCode":"PA","parameterName":"O3","latitude":39.95,"longitude":-75.151,"aqi":8}' data-lang="application/json"><pre><code lang="application/json">{&quot;dateObserved&quot;:&quot;2023-01-19 &quot;,&quot;hourObserved&quot;:12,&quot;localTimeZone&quot;:&quot;EST&quot;,&quot;reportingArea&quot;:&quot;Philadelphia&quot;,&quot;stateCode&quot;:&quot;PA&quot;,&quot;parameterName&quot;:&quot;O3&quot;,&quot;latitude&quot;:39.95,&quot;longitude&quot;:-75.151,&quot;aqi&quot;:8}</code></pre></div></div></div>
<p dir="ltr">
    <br>
</p>
<h3 dir="ltr">Example PM10 Data</h3>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">JSON</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code='{"dateObserved":"2023-01-19 ","hourObserved":12,"localTimeZone":"EST","reportingArea":"Philadelphia","stateCode":"PA","parameterName":"PM10","latitude":39.95,"longitude":-75.151,"aqi":19}' data-lang="application/json"><pre><code lang="application/json">{&quot;dateObserved&quot;:&quot;2023-01-19 &quot;,&quot;hourObserved&quot;:12,&quot;localTimeZone&quot;:&quot;EST&quot;,&quot;reportingArea&quot;:&quot;Philadelphia&quot;,&quot;stateCode&quot;:&quot;PA&quot;,&quot;parameterName&quot;:&quot;PM10&quot;,&quot;latitude&quot;:39.95,&quot;longitude&quot;:-75.151,&quot;aqi&quot;:19}</code></pre></div></div></div>
<p>
    <br>
</p>
<h3 dir="ltr">Example PM2.5 Data</h3>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">JSON</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code='{"dateObserved":"2023-01-19 ","hourObserved":12,"localTimeZone":"EST","reportingArea":"Philadelphia","stateCode":"PA","parameterName":"PM2.5","latitude":39.95,"longitude":-75.151,"aqi":54}' data-lang="application/json"><pre><code lang="application/json">{&quot;dateObserved&quot;:&quot;2023-01-19 &quot;,&quot;hourObserved&quot;:12,&quot;localTimeZone&quot;:&quot;EST&quot;,&quot;reportingArea&quot;:&quot;Philadelphia&quot;,&quot;stateCode&quot;:&quot;PA&quot;,&quot;parameterName&quot;:&quot;PM2.5&quot;,&quot;latitude&quot;:39.95,&quot;longitude&quot;:-75.151,&quot;aqi&quot;:54}</code></pre></div></div></div>
<p>
    <br>
</p>
<p><img style="width: 500px;" class="fr-fic fr-dib ls-is-cached lazyloaded" data-image="true" data-new="false" data-sizeformatted="130.9 kB" data-mimetype="image/jpeg" data-creationdate="1674834972918" data-creationdateformatted="01/27/2023 03:56 PM" data-type="temp" data-url="https://dz2cdn1.dzone.com/storage/temp/16670846-9723d474-15fd-4806-b410-74647fbe0d26.jpeg" data-modificationdate="null" data-size="130860" data-name="9723d474-15fd-4806-b410-74647fbe0d26.jpeg" data-id="16670846" data-src="https://dz2cdn1.dzone.com/storage/temp/16670846-9723d474-15fd-4806-b410-74647fbe0d26.jpeg" alt="Spring 1" src="https://dz2cdn1.dzone.com/storage/temp/16670846-9723d474-15fd-4806-b410-74647fbe0d26.jpeg"></p>
<p><img style="width: 500px;" class="fr-fic fr-dib lazyloaded" data-image="true" data-new="false" data-sizeformatted="179.6 kB" data-mimetype="image/jpeg" data-creationdate="1674834996844" data-creationdateformatted="01/27/2023 03:56 PM" data-type="temp" data-url="https://dz2cdn1.dzone.com/storage/temp/16670847-d2dc9d68-702b-4917-9d84-028b6925f7be.jpeg" data-modificationdate="null" data-size="179612" data-name="d2dc9d68-702b-4917-9d84-028b6925f7be.jpeg" data-id="16670847" alt="Spring 2" data-src="https://dz2cdn1.dzone.com/storage/temp/16670847-d2dc9d68-702b-4917-9d84-028b6925f7be.jpeg" src="https://dz2cdn1.dzone.com/storage/temp/16670847-d2dc9d68-702b-4917-9d84-028b6925f7be.jpeg"></p>
<h2 dir="ltr">Data Processing</h2>
<p><span data-preserver-spaces="true">In order to process the data collected, we used the Hazelcast Pulsar connector module to ingest data from Pulsar topics.</span></p>
<p><strong><em>Note</em></strong><span data-preserver-spaces="true">: you can use the same connector to write to Pulsar topics.&nbsp;</span></p>
<p><span data-preserver-spaces="true">Using Hazelcast allows us to compute various aggregation functions (sum, avg, etc.) in real-time on a specified window of stream items. The Pulsar connector uses the Pulsar client library, which has two different ways of reading messages from a Pulsar topic. These are Consumer API and Reader API; both use the builder pattern (for more information,</span><a href="https://github.com/hazelcast/hazelcast-jet-contrib/tree/master/pulsar" target="_blank">&nbsp;click here</a><span data-preserver-spaces="true">).</span></p>
<p><span data-preserver-spaces="true">In your pom file, import the following dependencies:</span></p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">XML</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="<dependency>

           <groupId>com.hazelcast</groupId>

           <artifactId>hazelcast</artifactId>

           <version>5.1.4</version>

       </dependency>

       <dependency>

           <groupId>com.hazelcast.jet.contrib</groupId>

           <artifactId>pulsar</artifactId>

           <version>0.1</version>

       </dependency>

       <dependency>

           <groupId>org.apache.pulsar</groupId>

           <artifactId>pulsar-client</artifactId>

           <version>2.10.1</version>

       </dependency>" data-lang="application/xml"><pre><code lang="application/xml">&lt;dependency&gt;

           &lt;groupId&gt;com.hazelcast&lt;/groupId&gt;

           &lt;artifactId&gt;hazelcast&lt;/artifactId&gt;

           &lt;version&gt;5.1.4&lt;/version&gt;

       &lt;/dependency&gt;

       &lt;dependency&gt;

           &lt;groupId&gt;com.hazelcast.jet.contrib&lt;/groupId&gt;

           &lt;artifactId&gt;pulsar&lt;/artifactId&gt;

           &lt;version&gt;0.1&lt;/version&gt;

       &lt;/dependency&gt;

       &lt;dependency&gt;

           &lt;groupId&gt;org.apache.pulsar&lt;/groupId&gt;

           &lt;artifactId&gt;pulsar-client&lt;/artifactId&gt;

           &lt;version&gt;2.10.1&lt;/version&gt;

       &lt;/dependency&gt;</code></pre></div></div></div>
<p>
    <br>
</p>
<p dir="ltr">&nbsp;We create a <code>PulsarSources.pulsarReaderBuilder</code> instance to connect to the previously started Pulsar cluster located at <code>pulsar://localhost:6650</code>.</p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Java</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code='StreamSource<Event>source = PulsarSources.pulsarReaderBuilder(

        topicName,

        () -> PulsarClient.builder().serviceUrl("pulsar://localhost:6650").build(),

        () -> Schema.JSON(Event.class),

        Message::getValue).build();' data-lang="text/x-java"><pre><code lang="text/x-java">StreamSource&lt;Event&gt;source = PulsarSources.pulsarReaderBuilder(

        topicName,

        () -&gt; PulsarClient.builder().serviceUrl(&quot;pulsar://localhost:6650&quot;).build(),

        () -&gt; Schema.JSON(Event.class),

        Message::getValue).build();</code></pre></div></div></div>
<p>
    <br>
</p>
<p dir="ltr">We then create a pipeline to read from the source with a sliding window and aggregate count before we write to logger:</p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Java</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code='Pipeline p = Pipeline.create();

p.readFrom(source)

 .withNativeTimestamps(0)

 .groupingKey(Event::getUser)

 .window(sliding(SECONDS.toMillis(60), SECONDS.toMillis(30)))

 .aggregate(counting())

 .writeTo(Sinks.logger(wr -> String.format(

         "At %s Pulsar got %,d messages in the previous minute from %s.",

         TIME_FORMATTER.format(LocalDateTime.ofInstant(

                 Instant.ofEpochMilli(wr.end()), ZoneId.systemDefault())),

         wr.result(), wr.key()))); 

JobConfig cfg = new JobConfig()

        .setProcessingGuarantee(ProcessingGuarantee.EXACTLY_ONCE)

        .setSnapshotIntervalMillis(SECONDS.toMillis(1))

        .setName("pulsar-airquality-counter");

HazelcastInstance hz = Hazelcast.bootstrappedInstance();

hz.getJet().newJob(p, cfg);' data-lang="text/x-java"><pre><code lang="text/x-java">Pipeline p = Pipeline.create();

p.readFrom(source)

 .withNativeTimestamps(0)

 .groupingKey(Event::getUser)

 .window(sliding(SECONDS.toMillis(60), SECONDS.toMillis(30)))

 .aggregate(counting())

 .writeTo(Sinks.logger(wr -&gt; String.format(

         &quot;At %s Pulsar got %,d messages in the previous minute from %s.&quot;,

         TIME_FORMATTER.format(LocalDateTime.ofInstant(

                 Instant.ofEpochMilli(wr.end()), ZoneId.systemDefault())),

         wr.result(), wr.key()))); 

JobConfig cfg = new JobConfig()

        .setProcessingGuarantee(ProcessingGuarantee.EXACTLY_ONCE)

        .setSnapshotIntervalMillis(SECONDS.toMillis(1))

        .setName(&quot;pulsar-airquality-counter&quot;);

HazelcastInstance hz = Hazelcast.bootstrappedInstance();

hz.getJet().newJob(p, cfg);</code></pre></div></div></div>
<p>
    <br>
</p>
<p dir="ltr">You can run the previous code from your IDE (in this case, it will create its own Hazelcast member and run the job on it), or you can run this on the previously started Hazelcast member (in this case, you need to create a runnable JAR including all dependencies required to run it):</p>
<div class="codeMirror-wrapper newest" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Shell</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="mvn package

bin/hz-cli submit target/pulsar-example-1.0-SNAPSHOT.jar
" data-lang="text/x-sh"><pre><code lang="text/x-sh">mvn package

bin/hz-cli submit target/pulsar-example-1.0-SNAPSHOT.jar
</code></pre></div></div></div>
<p dir="ltr">
    <br>
</p>
<p dir="ltr">To cancel the job and shut down the Hazelcast cluster:</p>
<div class="codeMirror-wrapper" contenteditable="false">
    <div contenteditable="false">
        <div class="codeHeader">
            <div class="nameLanguage">Shell</div><i class="icon-cancel-circled-1 cm-remove">&nbsp;</i></div>
        <div class="codeMirror-code--wrapper" data-code="bin/hz-cli cancel pulsar-message-counter

hz-stop" data-lang="text/x-sh"><pre><code lang="text/x-sh">bin/hz-cli cancel pulsar-message-counter

hz-stop</code></pre></div></div></div>
<p>
    <br>
</p>
<h2 dir="ltr">Conclusion</h2>
<p dir="ltr">In this article, we demonstrated how you can combine the strengths and advantages of various technologies to provide a unique developer experience and an efficient way of processing data in real-time at scale. We streamed air quality data from Apache Pulsar into Hazelcast, where we processed data in real-time. The rising trend in cloud technologies, the need for real-time intelligent applications, and the urgency to process data at scale have brought us to a new chapter of real-time stream processing, where latencies are measured, not in minutes but in milliseconds and submillisecond&rsquo;s.</p>
<p dir="ltr">Hazelcast allows you to quickly build resource-efficient, real-time applications. You can deploy it at any scale, from small-edge devices to a large cluster of cloud instances. A cluster of Hazelcast nodes shares the data storage and computational load, which can dynamically scale up and down. When you add new nodes to the cluster, the data is automatically rebalanced across the cluster, and currently running computational tasks (known as jobs) snapshot their state and scale with processing guarantees. Pulsar allows you to use your choice of messaging protocols to quickly distribute events between multiple types of consumers and producers and act as a universal message hub. Pulsar separates compute from storage, allowing for dynamic scaling and efficient handling of fast data. StreamNative is the company made up of the original creators of Apache Pulsar and Apache BookKeeper. StreamNative provides a full enterprise experience for Apache Pulsar in the cloud and on-premise.</p>
