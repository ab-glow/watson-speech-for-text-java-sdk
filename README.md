# watson-speech-for-text-java-sdk
How to run Watson speech for text in java
1 code for java to run speech for text
2 orignal code from Watson repository
3how i found out and more...

Follow the instructions from watson https://github.com/watson-developer-cloud/java-sdk#before-you-begin then come back here

1 For speech to text watson api to work in java in my case so is this code below of running working.
---------------------------------------------------------------------
```
SpeechToText service = new SpeechToText();
service.setEndPoint("<URL>");
  IamOptions options1 = new IamOptions.Builder()
  .apiKey("<iam_api_key>")
  .build();
 service.setIamCredentials(options1);

 File audio = new File("src/test/audio-file.FLAC");

 RecognizeOptions options = new RecognizeOptions.Builder()
   .audio(audio)
   .contentType(HttpMediaType.AUDIO_FLAC)
   .build();

 SpeechRecognitionResults transcript = service.recognize(options).execute().getResult();
 System.out.println(transcript);
```
1:1 Public main is required with throws FileNotFoundException
-------------------------------------------------------------------
2 below here is the origianal code before (which did not work for me) for comparison  purpose
----------------------------------------------------------------------------------------------
```
SpeechToText service = new SpeechToText();
IamOptions options = new IamOptions.Builder()
  .apiKey("<iam_api_key>")
  .build();
service.setIamCredentials(options);

File audio = new File("src/test/resources/sample1.wav");

RecognizeOptions options = new RecognizeOptions.Builder()
  .audio(audio)
  .contentType(HttpMediaType.AUDIO_WAV)
  .build();

SpeechRecognitionResults transcript = service.recognize(options).execute().getResult();
System.out.println(transcript);
```

3 This was a solution I found on my own when asking it on StackOverflow. Looking at the IBM doc for Watson API(SDK) was how I found out what the Watson repository was missing. Note that the API(SDK) guide for curl seems to go faster when comparing with java. In my experience, you also see the duration for how long for the audio to be done which java SDK API is missing by default. That is when running in this code. But I think you can add it to java in some way.
--------------------------------------------------------------
