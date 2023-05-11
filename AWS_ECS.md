# Amazon ECS 入門ハンズオン
- https://catalog.us-east-1.prod.workshops.aws/workshops/7ffc4ed9-d4b3-44dc-bade-676162b427cd/ja-JP

## Cloud9
cloud9 ip
18.183.231.93

ecr url
550710841574.dkr.ecr.ap-northeast-1.amazonaws.com/h4b-ecs-helloworld

プッシュコマンド
aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin 550710841574.dkr.ecr.ap-northeast-1.amazonaws.com

docker imageにTagの付与
docker build -t 550710841574.dkr.ecr.ap-northeast-1.amazonaws.com/h4b-ecs-helloworld:0.0.1 .

docker login
aws ecr get-login-password --region ap-northeast-1 | docker login --username AWS --password-stdin 550710841574.dkr.ecr.ap-northeast-1.amazonaws.com

dokcer push 
docker push 550710841574.dkr.ecr.ap-northeast-1.amazonaws.com/h4b-ecs-helloworld:0.0.1

dns
h4b-ecs-alb-834447303.ap-northeast-1.elb.amazonaws.com 


url=http:/h4b-ecs-alb-834447303.ap-northeast-1.elb.amazonaws.com/
while true; do TZ=JST-9 date; curl $url; sleep 1s; done