# JSONDataParser-Demo
This repository is added to demonstrate how we can parse the JSON data. It also include How we can download any content from web.

## How to Download content/file from web? 
So, for accessing any file from web We can use doInBackground( .. ) method of AsyncTask< .. >. 
I have made one **DownloadTask Class** which extends **AsyncTask< ... >** and that gives the implementation of method **doInBackground()** as following : 
```
public class DownloadTask extends AsyncTask<String, Void, String>{

        @Override
        protected String doInBackground(String... urls) {

            String result=""; // used to save the content
            URL url; // the webpage's url will be provided 
            HttpURLConnection urlConnection = null; // for connect/disconnect to web

            try {
                url = new URL(urls[0]); // we need only first argument as we are proving the web address into first argument

                urlConnection = (HttpURLConnection) url.openConnection(); // starting the communication
                InputStream in = urlConnection.getInputStream(); // using inputstream to save the data
                InputStreamReader reader = new InputStreamReader(in); // to read upcoming data
                int data = reader.read(); // final content word by word
                while (data!=-1){        // untill empty
                    char current = (char)data;   
                    result+=current;
                    data = reader.read();

                }
                return result;
            } catch (MalformedURLException e) {
                e.printStackTrace();
            } catch (IOException e) {
                e.printStackTrace();
            }
            return null;
        }
```
So, For giving implementation to doInBackground() method we need three basic things. we can store the data into string, we need URL object and also we need the HttpURLConnection object to access the methods of that class. 

**Note : _doInBackground() method does not interact with UI. so, If there is any UI requirements for example you want to update UI after getting content from web, there are two options (1) Use main thread (2) Use onPostExecute() method_**

