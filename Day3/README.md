## Using Template module to customize files before it is copied onto the ansible nodes
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook install-nginx-playbook.yml
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/1348fd18-dca0-45f9-9edc-21076c2d9cf3)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/908b4c6e-32fc-4a56-a4da-ccb35da14624)

## Lab - Building Custom Ubuntu Ansible Node Docker Image
```
cd ~/ansible-sep-2023
git pull
cd Day3/CustomDockerImages/centos
cp ~/.ssh/id_rsa.pub authorized_keys
docker build -t tektutor/ansible-centos-node:latest .
docker images
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/5798b6d4-8a74-4727-bc5f-7b0d581f911b)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/aa1a2846-7f61-4508-ac60-4bb9e628eafe)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/364387fc-3ad4-4fe9-8f58-e473aeca24c4)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/95acb054-0aaf-4909-94fd-c8bbd6442d5f)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/27a0d0b8-0943-4460-beaf-b243774e321b)

## Lab - Creating centos1 and centos2 containers using the newly build custom centos docker image
```
docker images
docker run -d --name centos1 --hostname centos1 -p 2003:22 -p 8003:80 tektutor/ansible-centos-node:latest
docker run -d --name centos2 --hostname centos2 -p 2004:22 -p 8004:80 tektutor/ansible-centos-node:latest
docker ps
```
Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/19b9a5c6-c594-447f-be03-579f5b02c938)

## Lab - Testing if we are able to SSH into the centos1 and centos2 containers
```
docker ps
ssh -p 2003 root@localhost
exit
ssh -p 2004 root@localhost
exit
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/e356e05b-de00-44ef-9a1a-73694760d771)

## Lab - Suppressing host key checking while doing ssh into ansible nodes
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
cat ~/ansible.cfg
ansible all -m ping
cat ~/ansible.cfg
ansible all -m ping
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/9688c1fd-b30d-4510-8b3a-71de5fcf27ee)

![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/093cc89c-25f7-40c3-befb-f30f386970e0)

## Lab - Executing install nginx playbook in Ubuntu and CentOS ansible nodes in a conditional fashion
### Optional
```
docker cp centos1:/etc/nginx/nginx.conf .
```

Now you may proceed as shown below
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook install-ngxin-playbook.yml
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/ab70c95d-2ee4-4038-9b65-047120a31685)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/632ebd9d-0fd0-40a6-9e75-5ec46ca8dc28)

## Lab - Understanding the refactored install nginx playbook
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks/after-refactoring
ansible-playbook install-nginx-playbook.yml
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/9d37fe20-1e29-4aee-b896-60f066a321f3)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/5b056277-af02-4b96-adc0-33cc48bf8d2a)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/388189a7-86e0-444e-b6be-df12d44b8d1d)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/03e98ef7-55cf-41ae-9903-b439db8781d8)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/249feb41-028a-42a0-843c-8b7d9e86c358)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/a1d6d6a6-e3f2-46ea-ba91-013d72c5202f)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/b1ab05ce-346f-43d4-b5fb-3c9c82cbe30b)

## Lab - Limitting the playbook execution only on specific ansible node/nodes
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks/after-refactoring
ansible-playbook install-nginx-playbook.yml --limit=ubuntu1
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/75869c1c-975b-4df0-bb6e-3ae87a1a4b9c)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/547ea67d-9241-4b4b-96dd-b61a42c6b77f)

## Lab - Passing extra arguments to playbook
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook passing-extra-arg-to-playbook.yml
ansible-playbook passing-extra-arg-to-playbook.yml -e jdk_path=/usr/lib/jdk17
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/31c9e685-2eb5-40ef-8907-c9bc16346a93)

## Lab - Invoking playbook from other playbook
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook invoking-playbook-from-playbook.yml
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/d0a06519-f279-4771-8735-8cb70203e111)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/e8ed32d2-5ab1-499f-88a4-64e96c69e0ef)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/fcb023ee-8fa0-464e-b95b-6b878ee6a963)

## Lab - Using service module in ansible playbook
When it prompts for password, type rps@12345
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook managing-service-via-playbook.yml --ask-become-pass
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/35fb3b00-d4fd-496d-a91b-867c9811d1cd)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/bd84a84f-5319-4da6-a382-230c8e355018)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/dfc2141d-6171-4059-bb01-a045558b8ceb)

## Lab - Using command module in ansible playbook
When it prompts for password, type rps@12345
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook using-command-module-in-playbook.yml --ask-become-pass
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/96c57cc4-b079-4311-8988-b942390a2392)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/9fcb5000-73cd-4c9c-8a72-c51995ebbe1a)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/da4ca6ee-07e8-41f7-8b6e-b4c00f44ffed)

## Lab - Provisioning containers using ansible playbook
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook provision-docker-container-using-playbook.yml
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/a1d838d1-f607-4b92-843d-7702defc81f6)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/4ce64f37-f1af-4f4f-9429-73126e912e96)

## Lab - Using dynamic inventory in ansible playbooks
```
cd ~/ansible-sep-2023
git pull
cd Day3/playbooks
ansible-playbook install-nginx-playbook.yml
```

Expected output
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/897ca5c8-a483-41f8-b845-35486857d71c)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/160a873b-9bbf-4243-a99d-cbf73b75d409)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/ea336910-ebcf-4e1e-91d2-913279fbeda3)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/dc146de0-0cef-4c29-a5f9-dc59da6e655a)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/ef1869b5-fbfd-4fa7-aa57-7c3fea180698)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/e2a6d966-4a8f-4a4e-8cc1-456314b9531e)
![image](https://github.com/tektutor/ansible-sep-2023/assets/12674043/fa9da95e-52e3-469c-a979-f2ba4b9dadb7)
