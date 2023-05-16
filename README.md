1. Downloading the WordPress chart and installing it with Helm

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/2cea28dd-6431-4f61-a279-b2b1897b870e)

2. I used <i>helm dependency build</i> - to build the dependencies from the "Bitnami" chart repository and download the required files:
 
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/edd9ceae-418d-4220-97ea-c40822ace51c)
- I was interchangeably using Git Bash and PowerShell to execute the commands, since some of the commands weren't working in my powerShell

3. Changing the service type to ClusterIP on line 534

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/3f66239e-7c5f-470a-9262-829b1cdd4e29)

* I found another command that can be used to change the service type and <strong>patch the chart</strong>:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/5fe8752d-746b-4026-a63d-1af34086bc38)


4. Using kubectl get svc to get the services I've created so far (I will be using wordpress-chart for the purpose of this project)

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/49801b5e-d420-47d7-8927-9b2d0f9aa5a1)
- we can see that the chart has a MariaDB dependency

5. The pods are up and running in my Kubernetes cluster

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/f6e6695b-e618-4f7d-bc7e-71f9be5ceb76)

- checking the yaml file of my service:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/1c49c727-546e-4271-97f0-ea740091f398)

6. Create a Jenkins pipeline
 - I used the help of ChatGPT to generate the script for the namespace condition and installation of the WordPress Helm chart. 
 - I have uploaded the contents of the script in the Jenkins file in my repo.


The first step was verified, but I encountered an issue with the second part of the script - the deployment failed
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/fcea40dd-e81f-4291-8f96-a4734b76158f)
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/bde857c9-b759-47e6-80ac-871e53582ed2)



7. I had to forward the port to 27107 so that I can access the site, since I had some issues with the ports
 ![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/f8f0c57b-8b7b-48ab-8e76-0264fddf4d59)
 - to resolve this issue, I used the command <em>kubectl port-forward svc/wordpress-chart 27017:80</em>

8. This way, I could access the site on 127.0.0.1:27017


10. ![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/e1b6db17-b9e7-412c-9ccc-a15b21a89d80)
- And log in with the credentials
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/7e74e44b-0079-4b87-9103-9a1b01455910)

Here is the final result:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/b86a1c54-83a3-423e-924a-9f7ab0744869)


