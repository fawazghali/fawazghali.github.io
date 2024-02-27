---
layout: post
title: How To Get Started With the Hazelcast Viridian Serverless
subtitle: In this tutorial, you will learn how to connect a client to a cluster and use SQL to query data in the cluster.
gh-repo: daattali/beautiful-jekyll
gh-badge: [star, fork, follow]
tags: [cloud, serverless]
comments: true
author: Fawaz Ghali
---

The Hazelcast Serverless means that Hazelcast manages the cloud infrastructure for you. Each Viridian Serverless cluster is an independent deployment of the Hazelcast Platform in a Kubernetes container. This design guarantees resource isolation, prevents resource stealing and provides isolated network access. Viridian Serverless clusters come in two types:1) Development: Capped storage. You can store at most 1 GiB of data; and 2) Production: Uncapped storage. The cluster scales as you add or remove data. In this tutorial, you’ll learn how to connect a client to a cluster and use SQL to query data in the cluster.

Before You Begin
You need the following:

A Hazelcast Viridian account
Access to a command prompt such as Terminal for Mac or Powershell for Windows.
Step 1. Start a Viridian Serverless Development Cluster
Development clusters are for fast, iterative development while you prototype your application. To create a development cluster, do the following:

Sign into the Hazelcast Viridian console
Click Create New Cluster
Click Create Development Cluster
Update the cluster name if you want to. You cannot change the cluster name after the cluster is created.
Click Create Cluster
Wait while your cluster is created. When the cluster is up and running, a Quick Connection Guide is displayed with instructions for connecting a sample client to it.
Step 2. Connect a Sample Client
To connect to your Viridian Serverless cluster, you need a Hazelcast client. The cluster comes with sample clients that are preconfigured to connect to your cluster and add some sample data to a map. A map is an in-memory, key/value data structure that is often used as a cache.

Before you begin:

Install Java 8-17 and set the JAVA_HOME environment variable to the location of your JRE.
If you’ve followed the onscreen Quick Connection Guide, jump straight to step 6.
In the Quick Connection Guide on your cluster, click on the Java icon and then click Download.
Extract the ZIP file
From a command prompt, change to the root directory of the extracted files
Execute one of the following commands to run your client:
If you use Linux or Mac, execute: ./mvnw clean compile exec:java@client-with-ssl
If you use Windows, execute: mvnw.cmd clean compile exec:java@client-with-ssl
To query data in the cities map, you need to create a mapping to it. In step 3 of the Quick Connection Guide on your cluster, click Dashboard.
In Cluster Details, click Management Center, and then from the top toolbar, click SQL Browser.
Paste the following command into the SQL browser and execute it.
 
__key VARCHAR,

country VARCHAR,

city VARCHAR,

population INT)

type IMap OPTIONS('keyFormat'='varchar', 'valueFormat'='json-flat');


Step 3. Query the Cache with SQL
Now that you have some data in your cluster, you can query it using SQL. If you’re using the CLI, enter the following queries in the SQL prompt. If you’re using a client library, enter the following queries in the SQL browser.

Execute the following SELECT statement to query all data in the map.
SELECT * FROM cities;

The results are in random order because the data is distributed across the cluster.

Order the results by the key.
SELECT * FROM cities ORDER BY __key; 

Now you see the results start from key 1 and end with key 8. 

Query only the countries by filtering on the countries column.
SELECT country FROM cities;

Query only the cities by filtering on the cities column.
SELECT city FROM cities;

Change the output to display cities first in alphabetical order.
SELECT city, country FROM cities ORDER BY city;

Use a filter to display only countries where the name of the city is at least 11 characters long.
SELECT country FROM cities WHERE LENGTH(city) >= 11;

Use another filter to display only cities beginning with the letter 'L' where the length is greater than 6.
SELECT city FROM cities WHERE city LIKE 'L%' AND LENGTH(city) > 6;

Summary
In this tutorial, we learned how to connect to the Hazelcast Viridian Serverless and use SQL to query data. It is possible to connect to the Viridian using Java, Node.js, Python, .NET, C++, and Go. Once connected, you can manage your cluster through the Management Center. Hazelcast allows you to quickly build resource-efficient, real-time applications. You can deploy it at any scale, from small-edge devices to a large cluster of cloud instances. A cluster of Hazelcast nodes share both the data storage and computational load, which can dynamically scale up and down. When you add new nodes to the cluster, the data is automatically rebalanced across the cluster, and currently running computational tasks (known as jobs) snapshot their state and scale with processing guarantees.
