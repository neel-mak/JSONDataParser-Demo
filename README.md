# JSONDataParser-Demo
This repository is added to demonstrate how we can parse the JSON data. It also include How we can download any content from web.

_I am just donwloading all the content as String (assume as a large text file). So, I have done accordingly. It's just to understand the functionality of doInBackground() method and How we can use that._

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

## How to parse JSON data?
So, for any JSON data, we cna use JSONObject to handle the data, extract any individual type of data, manage the JSON array or whole lot of stuff. 
I have demonstrated the use of JSONObject like how we can capture the main opbject(array) and then If you want to process/get individual data, use **JSONObject.getString("")** that can give us the individual array element. //Still there are bunch of options available. 

For example,
_I have include the example related to make API calls to openweathermap.org website to get London's weather info_

```
protected void onPostExecute(String result) {
            Log.i("Donwloaded Content:",result);

            try {
                JSONObject jsonObject = new JSONObject(result);
                String weatherInfo = jsonObject.getString("weather");
                Log.i("Weather Details:",weatherInfo);


                JSONArray arr = new JSONArray(weatherInfo);
                for(int i=0;i<arr.length();i++){
                    JSONObject object = arr.getJSONObject(i);
                    Log.i("Individual Content:",object.getString("main"));

                }
            } catch (JSONException e) {
                e.printStackTrace();
            }
        }
```
As you can observe that using JSONArray we can read multiple objects and also extract their individual data-value.
As I mentioned earlier, These is the one way of possible all options. 

I hope this repo helped you, Enjoy ur day!!!
