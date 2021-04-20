# petclinic
Petclinic is a Springboot Application and can run as a Docker conatiner . 

# Prerequisites : 
1) It Connects to the MYSQL database, make sure database petclinic exists. 
2) username and password for database to be configured in application.properties file.

# To run Application 
git clone https://github.com/dewangsaurabh/petclinic.git
cd petclinic
mvn clean install -DskipTests=true (unit test cases are not configured yet)
Java -jar target/*.jar

# To run as docker
Docker build -t <tag_name> .
docker run mysql 
docker run <tag_name> -p 8080:8080

# To deploy on GKE platform.
1) Deploy using service account. 
   A) Download .json key format of service account.
   B) Create Secret using command kubectl create secret generic sa-secret --from-file=service_account.json=<file_path>
  
2) Update MySQL connection name in deployment.yaml.

3) Kubectl apply -f DEV/

# CICD Pipeline Configuration. 
1) Create credentials (username with password) and id docker_creds. 
2) update cluster name in stage "deploy" to get correct credentials.
