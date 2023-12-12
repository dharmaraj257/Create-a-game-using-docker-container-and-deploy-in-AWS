
# Create a game using docker container and deploy in AWS.

Create a game using docker image containerize game and docker containerized application deploy in AWS Cloud using elastic beanstalk Service. 

Prerequisites 
1.	Install docker in your local system 
2.	Aws account 

Step 1: Used 2048 GitHub repository to get the game file for containerization.
Game repository: https://github.com/gabrielecirulli/2048.git

Step 2: Create a docker file.

Dockerfile
```Dockerfile
FROM ubuntu:22.04

RUN apt-get update
RUN apt-get install -y nginx zip curl

RUN echo "demon off;" >>/etc/nginx/nginx.conf
RUN curl -o /var/www/html/master.zip -L https://github.com/gabrielecirulli/2048.git
RUN cd /var/www/html/ && unzip && mv 2048-/* . && rm -rf 2048

EXPOSE  80

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]  

```
Step 3: Build a docker image using Docker file.
```
docker build -t dharmaraj257/2048-game .
```
Step 4: Run docker Container using docker image.
```
docker run -d -p 80:80 dharmaraj257/2048-game
```
output:
![Screenshot (18)](https://github.com/dharmaraj257/aws-project/assets/100831265/2a72c5fd-3784-421c-970d-f7030b960ef3)


Step 5: Deploy Docker Container(game) on AWS
1.	Go to the Aws Management Console log in.
2.	Search Aws elastic beanstalk and click create application.
3.	Give an application name 2048 and add application tag 
4.	 select platform docker used recommended version and in application code select upload your code give version label 2048-source.
5.	Select local file and upload your Docker file and select single instance.
6.	Click next and in service access select Create and use new service role.
7.	Give a service role name select keypair and add Ec2 instance profile.
8.	Click next and select vpc and In Instance setting click activate public Ip address
9.	Select all Subnets. click next and leave default setting in instances
10.	Click next review the application and submit
11.	It will take time to launch service elastic beanstalk.
12.	Copy domain link paste in browser and your application deploy successfully.

Output:


![Screenshot (22)](https://github.com/dharmaraj257/aws-project/assets/100831265/52ad1c26-0603-4855-a814-929abe00dca6)







