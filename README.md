# Greenhouse web hook setup


## 1.Data and keys config 
#### 1.1. Make sure you have correct tenant data in database.
#### 1.2. Make sure the api key you have in the ats GH(admin panel) is sendbox key, not production one.
 _http://#tenant.localhost:8000/admin/ **>** Atss **>** GH_

## 2.Setup Ngrok
#### 2.1. Download and install Ngrok: https://ngrok.com/download.
#### 2.2. Sign in to: https://dashboard.ngrok.com/login so you can see private settings and current tunel connections.
#### 2.3. Find authtoken in your dashboard - getting started tab.
#### 2.4. Open terminal/cmd and add authtoken to ngrok.
```sh
> ngrok authtoken <<authtoken>>
```
#### 2.5. In terminal/cmd create tunnel endpoint:
```sh
> ngrok http -host-header=rewrite test.my-domain.com:8000
> #example: ngrok http -host-header=rewrite robinhood.localhost:8000
```
#### 2.6. In browser paste **https** url address you got after running command above.
```sh
> #example: https://cc75-80-74-161-168.ngrok.io
```
 - If you get"_**502(Bad Gateway)**_" in terminal/cmd or "_**Failed to complete tunnel connection**_" error in browser, close the connection and run below command instead of command in **_2.5._** step.
   ```sh
   > ngrok http -host-header=test.my-domain.com:8000
   > #example: ngrok http -host-header=robinhood.localhost 8000
   ```
#### 2.7. To check if everything is working you can go to **https** url address you got from ngrok  and add "/api" to url. You should see Django Rest Framework -API ROOT
```sh
> #example: https://cc75-80-74-161-168.ngrok.io/api
```

## 3.Greenhouse web hook setup
#### 3.1. Go to Greenhouse login page: https://app.greenhouse.io/users/sign_in.
#### 3.2. Login with sandbox account - you can find credentials in 1Password.
#### 3.3. Go to: Configure **>** Dev Center **>** Web Hooks **>** Web Hooks. There you can create new or modify already existing web hooks.
#### 3.4. Steps for creating web hook: 
 - "Name this web hook" - You can name web hook whatever you want, but name should be descriptive as possible.
 - "When" - choose event that will trigger web hook.
 - "Endpoint URL" - Paste **https** url address you got from ngrog(greenhouse does not support http) and add web hook endpoint that you want to hit: 
    ```sh
    > #example: https://cc75-80-74-161-168.ngrok.io/api/gh-offers/hooks/new
    ```
 - "Secret key" - This is Greenhouse Hook Key you can find in Ats(Django Admin) - step **_1.2._**.
 - "Error recipient email" - Add your email.
 - "Disabled" - Set to "No".
 - Click "Create Web hook".

# You are all set up.
