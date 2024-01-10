# streamlit-on-azure
demonstrate  streamlit app deploy on azure

## Context
As I recently faced this question in my work, I decided did some research how to deploy streamlit in Azure

Why deploy streamlit on azure?
Streamlit has managed services with Snowflake , however it is only GA with AWS. so if you are azure user , you would need to find alternative to deploy

## Process step
Process step is referencing the step here : https://learn.microsoft.com/en-us/answers/questions/1470782/how-to-deploy-a-streamlit-application-on-azure-app

1. Create an Azure App Service with B1 SKU or higher, as the free version does not support Streamlit.
2. Choose Python v3.10 or above for Streamlit in the App Service.
3. Choose Linux as the operating system for the App Service.
4. Use "Code" option
5. Make sure your code folder has a requirements.txt file with all the dependencies.
6. Create a bash script run.sh, and write the following command in it:
    ```python -m streamlit run hello.py --server.port 8000 --server.address 0.0.0.0```
7. Use port 8000 because Azure App Service by default exposes only 8000 and 443 ports.
8. Open Visual Studio Code and install the Azure Extension Pack (pack name: "Azure Tool" (as at 10 Jan 2024))
9. Log in to Visual Studio Code with your Azure account.
10. Use the Azure App Service: Deploy to Web App command in Visual Studio Code and select your App Service name.
11. Wait for deployment to be finished.
12. Go to the Azure portal and update the Startup Command configuration for the App Service and set the value to run.sh. You can find this configuration inside App Service > Settings > Configurations > General settings.
13. Wait for some seconds and visit the application URL. Congratulations! You have successfully deployed your Streamlit application to the Azure App Service.


## Notes
1. Streamlit example code is based on this example multiple page app: https://docs.streamlit.io/get-started/tutorials/create-a-multipage-app


## Other considerations
1. If we want to secure the app for internal use. We would need to do some work using PrivateLink
   https://learn.microsoft.com/en-us/azure/app-service/overview-private-endpoint

[![App Private Link](https://learn.microsoft.com/en-us/azure/app-service/media/overview-private-endpoint/global-schema-web-app.png)]
