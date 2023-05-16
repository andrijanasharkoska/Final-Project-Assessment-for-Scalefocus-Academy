<h3>1. Downloading the WordPress chart and installing it with Helm<h3>

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/2cea28dd-6431-4f61-a279-b2b1897b870e)

<h3>2. I used <i>helm dependency build</i> - to build the dependencies from the "Bitnami" chart repository and download the required files:</h3>
 
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/edd9ceae-418d-4220-97ea-c40822ace51c)
- I was interchangeably using Git Bash and PowerShell to execute the commands, since some of the commands weren't working in my powerShell

 <h3>3. Changing the service type to <i>ClusterIP</i> on line 534</h3>

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/3f66239e-7c5f-470a-9262-829b1cdd4e29)

* I found another command that can be used to change the service type and <strong>patch the chart</strong>:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/5fe8752d-746b-4026-a63d-1af34086bc38)


<h3>4. Using kubectl get svc to get the services I've created so far</h3> (I will be using wordpress-chart for the purpose of this project)

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/49801b5e-d420-47d7-8927-9b2d0f9aa5a1)
- we can see that the chart has a MariaDB dependency

 <h3>5. The pods are up and running in my Kubernetes cluster</h3>

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/f6e6695b-e618-4f7d-bc7e-71f9be5ceb76)

- checking the yaml file of my service:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/1c49c727-546e-4271-97f0-ea740091f398)

<h4>6. Create a Jenkins pipeline</h4?
 - I used the help of ChatGPT to generate the script for the namespace condition and installation of the WordPress Helm chart. 
 - I have uploaded the contents of the script in the Jenkins file in my repo.

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/e0e45dfd-351a-453b-aaa9-f284a96bd5f7)


- And I've created the pipeline, and used the generated script for the Pipeline Definition

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/5104d208-88a9-4977-b295-708a1244b1b4)

<h4><i>Errors that I've got:</i><h4>
 
 <i>1) The Chart.yaml file is missing</i>
 
 ![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/e91155bf-1e03-4bde-aadf-6293f883d21c)


 
 <i> - Here's the error with the namespace I got: </i>
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/1de590de-86d7-471b-9dad-79a34308465d)

  <i>- Since I was executing the code several times, and I used another pipiline to fix the errors, so I can have a clean pipeline for the final project,
   I got an error that the namespace <strong>"wp"</strong> and the variable <strong>"releaseName"</strong> with the same value was already in use. 
   To fix this, I used "wp1" and I've changed the releaseName variable to 'final-project-wp-scalefocus1'just for the sake of finalizing the project. 
   The script was working with the "wp" namespace in another pipeline, and I will be providing it with th the <strong>"wp"</strong> and <strong>"final-project-wp-scalefocus"</strong> as values.</i>
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/6b8361a1-969a-4b04-a8f9-cd99ea87c9cd)

![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/b8bb022d-eb4b-4dec-9b7d-d09fae489a52)



The first step was verified, but I encountered an issue with the second part of the script - the deployment failed
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/fcea40dd-e81f-4291-8f96-a4734b76158f)
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/bde857c9-b759-47e6-80ac-871e53582ed2)

The path was not correctly specified, as we can see from the previous step as well:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/5dd31f2e-20a7-4e50-a579-b32927dc0d86)

 
 
Finally, I was able to create and execute the pipeline with no errors:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/250a3aec-4cbf-434a-8861-65a774da36d1)
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/77668277-0206-4934-8982-88de9fee42e9)


<h4>7. I had to forward the port to 27107 so that I can access the site, since I had some issues with the ports</h4>

 
 ![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/207f6978-b126-46bd-9881-48e173ad4aff)
 
 - to resolve this issue, I used the command <em>kubectl port-forward svc/wordpress-chart 27017:80</em>

 
 <h4>8. This way, I could access the site on 127.0.0.1:27017</h4>


![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/e1b6db17-b9e7-412c-9ccc-a15b21a89d80)
- And log in with the credentials
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/7e74e44b-0079-4b87-9103-9a1b01455910)

Here is the final result:
![image](https://github.com/andrijanasharkoska/Final-Project-Assessment-for-Scalefocus-Academy/assets/125911121/b86a1c54-83a3-423e-924a-9f7ab0744869)


