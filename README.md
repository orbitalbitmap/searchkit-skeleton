
Useful Links for Elasticsearch
Youtube playlist: https://github.com/LisaHJung/Beginners-Crash-Course-to-Elastic-Stack-Series-Table-of-Contents
Beginner guy repo: https://github.com/LisaHJung/Beginners-Crash-Course-to-Elastic-Stack-Series-Table-of-Contents


Folowed this guide for the local installation process: https://dev.to/elastic/downloading-elasticsearch-and-kibana-macos-linux-and-windows-1mmo (Link also found in part 1 of the beginner repo)

Setting up local ElasticSearch instance
1. Download Elasticsearch locally:  https://www.elastic.co/downloads/elasticsearch
2. Unzip contents to a location of your choosing
3. In a terminal, cd into the the unziped elasticsearch-7.16.2 folder 
4. In a terminal, run [bin/elastic] to get it running
5. In a new terminal, run curl http://localhost:9200 to check to see if Elastic search is running

Set up local Kibana
1. Download Kibana locally: https://www.elastic.co/downloads/kibana?S_TACT=
2. Unzip contents to a location of your choosing
3. In a terminal, cd into the kibana folder that was just unzipped
4. After Elasticsearch is up and running, ina terminal run [bin/kibana]
5. Open broweser to http://localhost:5601 to make sure Kibana is running and connected to Elasticsearch

Test Elasticsearch and Kibana connection
1. Go to the Dev Tools on the side menu under Management (Its close to th bottom of the side menu)
2. In the console on the Dev Tools page, in Kibana, run GET _cluster/health to check to see if the cluster is up and running the response should similar to this:
  {
    "cluster_name" : "elasticsearch",
    "status" : "yellow",
    "timed_out" : false,
    "number_of_nodes" : 1,
    "number_of_data_nodes" : 1,
    "active_primary_shards" : 30,
    "active_shards" : 30,
    "relocating_shards" : 0,
    "initializing_shards" : 0,
    "unassigned_shards" : 8,
    "delayed_unassigned_shards" : 0,
    "number_of_pending_tasks" : 0,
    "number_of_in_flight_fetch" : 0,
    "task_max_waiting_in_queue_millis" : 0,
    "active_shards_percent_as_number" : 78.94736842105263
  }


If somethinglike the above is displayed, then everything is set up and ready to go.   NOTE: By default there is no security for the cluster and anyone could potentially access if, below are instructions for setting up the security.


Setting up security for Elasticsearch
1. If any instance of Kibana or Elasticsearch is running, close them.
2. In the elasticsearch-7.16.2 open he config folder and then open the elasticsearch.yml file to edit
3. Add the following rule to the elasticsearch.yml file [xpack.security.enabled: true], without the brackets, and save
4. After saving the file, run elasstic search through the terminal with [bin/elasticsearch] (the file can be closed at this time)


Now its time to set the the passwords for the built-in users
1. Open a new terminal to the root elasticsearch-7.16.2 folder and run the command [bin/elasticsearch-setup-passwords interactive] <—————— the interactive flag allows you to set the passwords in the terminal.  REMEMBER THE PASSWORDS FOR EACH BUILT-IN USER
2. In the kibana folder, open up the kibana.yml file found in the config folder
3. Inside the kibana.yml file add [elasticsearch.username: “kibana_system”], without the brackets, and save the file
4. After saving the kibana.yml file, run the follwoing command to set up a keystore for kibana: [bin/kibana-keystore create]
5. Then run [bin/kibana-keystore add elasticsearch.password] to add the password for Elasticsearch into the Kibana keystore, you should be prompted to enter the password
6. Once all the above is done, run [bin/kibana] from the root kibana folder, everything should be running just fine

Add security 
To add security, open up the kibana.yml file find in the root kibana folder’s config folder, and add this to it: [xpack.security.encryptionKey: “THIS_STRING_MUST_BE_AT_LEAST_32_CHARACTERS”]


If you intend to run elasticsearch through a node.js client, you might need to add a user
1. Through the Kibana dashboard, click the searchbar in the top navbar and type in user
2. Click on the option that says: “Security / Users” with “Management” underneath it
3. Click the blue “+ Create User” and fill out the information for the user. (These can be, and were, used for a conenction from node.js to Elasticsearch)



React and Searhbox Skeleton Setup
1. Run npx create-react-app@latest searchbox-skeleton to create the React folder and files for the project
2. Start the react app with npm start
3. Install react-searchbox using [npm install @appbaseio/react-searchbox]
4. 1/10/22 Ran into react and react-searchbox compoatablity issue
