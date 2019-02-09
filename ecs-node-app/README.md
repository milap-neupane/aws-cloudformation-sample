Steps to deploy a node application

1. Create a node app
2. Containerize the node app
3. Loadbalancer(Cloudformation)
4. Loadbalancer Listner(Cloudformation)
5. Default target group(Cloudformation)
6. Load Balancer Listner Rule(Cloudformation)
7. Target group for es service
9. Service
8. Cluster
10. Task
11. IAM roles for task
12. CloudWatch group for task

## Steps to deploy a node application 

### [Step 1] Create a node app
-----------------------------

Create a directory ecs-node-app

```
$ mkdir mkdir ecs-node-app
$ cd ecs-node-app
```

Initialize node app
```
$ npm init
```
Install express as a server

```
$ npm install express --save
```

create a file server.js 
```
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(port, () => console.log(`Example app listening on port ${port}!`))
```

Try running the node app:
```
node app.js
```
| load http://localhost:3000/ in browser


### [Step 2] Containerize the node app
------------------------------
Create a file named Dockerfile. See the content in dockerfile for details
Add a file `.dockerignore` and add some files that would not be included in the build

### [Step 3] Loadbalancer
Build a loadbalancer in cloudformation

```
LoadBalancer:
    Type: AWS::ElasticLoadBalancingV2::LoadBalancer
    Properties:
      Name: training-aws-lb
      Subnets:
      - Fn::ImportValue:
          !Join [":", [ !Ref EnvironmentName, "SubnetAZ1Public" ]]
      - Fn::ImportValue:
          !Join [ ":", [ !Ref EnvironmentName, "SubnetAZ2Public" ]]
      SecurityGroups:
        - !Ref LoadBalancerSecurityGroup
```
Add security group
