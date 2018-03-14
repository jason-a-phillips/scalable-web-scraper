# autoscaling-realtime-miner

The goal of this application is to create the proof of concept for an autoscaling cluster of Node.js workers, managed by a Node.js controller, and backed by a Postgres data store. The job of the application will be to find new information posted on things like social media pages, news sites, as well as online forums, in less than one minute after the content is posted, thus being quasi-real-time.

The idea is that a template could be provided to the controller which would then distribute work to available workers. As new work and/or new workers are added, the controller will automatically redistribute work to workers.

The problem that this design overcomes is that one Node.js worker service cannot discover new content from an unlimited number of sources and still maintain the 1-minute level of data freshness. HTTP responses and the subsequent requests for the more detailed meta data simply take too long, sometimes 10+ seconds to complete. To maintain one-minute freshness of our data and not have similar jobs collide, the work must be distributed to many workers. 

The application right now is a tightly-coupled cluster, due to the relationship between the Node.js services and the database. This will scale up to the point where the Postgres becomes the bottleneck. The next step to increase scalability might be to insert an API in front of the database and scale the database with replication, document storage or NoSQL solutions, etc.


