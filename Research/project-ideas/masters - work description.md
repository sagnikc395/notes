- watsonx.data ->
    - customer comes and provide data related services to the customer 
    - query the warehouse 
    - apachae kafka to ingest the data 
    - create , query and update the data lake for the customer.
    - RoR MIDDLEWARE , js frontned
    - gRPC server written in Go -> RoR calls it.
    - below the kubernetes cluster which runs the loads.
    - gRPC server will call the controller -> custom resources -> controller to manage those
    - call from frontend -> middleware -> backend(grpc server will preapre this) 
    - pass the call to the operator 
    - it will setup all the resources in the cluster 

- concept ->
    - presto -> query engine -> query multiple source -> one sql db / one s3 bucket in 1 query ->
        query across multiple different sources 
    - milvusdb -> vector db 
    - user can use a ingestion service(kafka) -> one presto to query one of the bucket or one sql 

- Middleware + grpc + cluster -> deployment of the changes.
- make the nevironemtn , make sure connection to all of the services
- nodes are being provisioned -> presto engine (one container)
    - create services 
    - create ingress 
    - make sure it has everything it needs to run 
    - hive metastore 
    - auth shit 
    - wrapper around the engine is fine.