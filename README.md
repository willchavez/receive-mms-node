#Run twilio app for receiving messages, and using ngrok, to use on OBS

First you need to install [Node.js](http://nodejs.org/).

To run the app locally:

1. Clone this repository and `cd` into it

   ```bash
   git clone git@github.com:TwilioDevEd/receive-mms-node.git && \

   cd receive-mms-node
   ```

1. Install dependencies

   ```bash
   npm install -g yarn && \
   yarn install
   ```

1. Copy the sample configuration file and edit it to match your configuration

   ```bash
   $ cp .env .env.local
   ```

   You can find your `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` in your
   [Twilio Account Settings](https://www.twilio.com/console).
   You will also need a `TWILIO_PHONE_NUMBER`, which you may find [here](https://www.twilio.com/console/phone-numbers/incoming).

   Run `source .env.local` to export the environment variables

1. Run the application

   ```bash
   yarn start
   ```

   Alternatively you might also consider using [nodemon](https://github.com/remy/nodemon) for this. It works just like
   the node command but automatically restarts your application when you change any source code files.

   ```bash
   yarn global add nodemon && \
   nodemon index.js
   ```

1. Check it out at [http://localhost:3000](http://localhost:3000)

To get the app onto an ngrok server do the following

1. Sign up for an ngrok account at [ngrok.com](https://ngrok.com/). Download the client onto your computer. Copy the `.app` file that is in your Applications folder and place it in your project folder.
1. While the application is running, in another terminal window, navigate to the project folder.
1. run `./ngrok http 3000`
1. The output should look something like this

   ```
   ngrok by @inconshreveable                          (Ctrl+C to quit)

   Session Status                online
   Account                       Will Chavez (Plan: Free)
   Version                       2.3.35
   Region                        United States (us)
   Web Interface                 http://127.0.0.1:4040
   Forwarding                    http://b58686d3.ngrok.io -> http://lo
   Forwarding                    https://b58686d3.ngrok.io -> http://l

   Connections                   ttl     opn     rt1     rt5     p50
                             6533    0       0.89    0.42    0.93

   HTTP Requests
   -------------
   ```

1. Save the https url .

Now we have to set up the webhook on your twilio account.

1. Go to [twilio.com/console](https://www.twilio.com/console)
2. Go to 'All Products & Services'

   ![Screen Shot 2020-03-22 at 5.51.03 PM.png](https://images.zenhubusercontent.com/5bedbecdf7b9997909d9652c/cc7d981d-c7b8-4362-8e87-afcb2e7c3b70)

3. Go to Phone Numbers
   ![Screen Shot 2020-03-22 at 5.53.07 PM.png](https://images.zenhubusercontent.com/5bedbecdf7b9997909d9652c/eaaf63b2-f779-446e-8572-ec7b31012d61)

4. Click on your phone number
   ![Screen Shot 2020-03-22 at 5.53.17 PM.png](https://images.zenhubusercontent.com/5bedbecdf7b9997909d9652c/8c031922-110e-485f-9528-48079f7964d5)
5. Paste your link in the following space, and add `/incoming` to the end of that url. It should look something like `http://b123456.ngrok.io/incoming`
   ![Screen Shot 2020-03-22 at 5.53.34 PM.png](https://images.zenhubusercontent.com/5bedbecdf7b9997909d9652c/52a22c82-adcd-4d6c-90e1-fbd6f03e03f1)
6. Save and text an image to your twilio number. You should see the image show up in your `/public/mms_images/` folder soon.

Point OBS to look at that folder.
