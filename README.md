# Python_and_CURL
Communication RESTFUL service with Python and CURL

<p align="center" width="100%">
    <img width="25%" src="https://github.com/jkaewprateep/Python_and_CURL/blob/main/Python.jpg">
    <img width="24%" src="https://github.com/jkaewprateep/Python_and_CURL/blob/main/Curl_command.jpg">
    <img width="19%" src="https://github.com/jkaewprateep/Python_and_CURL/blob/main/kid_21.jpg">
    <img width="21.5%" src="https://github.com/jkaewprateep/Python_and_CURL/blob/main/kid_33.jpg"> </br>
    <b> Communication using CURL command for RESFUL services protocol negotiation and transmission </b> </br>
    <b> ( Picture from Internet ) </b> </br>
</p>
</br>
</br>

🧸💬 We selected to use the CURL command because it is a standard application for communication HTTP, readable messages, and RESTFUL web service protocol as it passed security policy for wide area networks and communication application best practices in many customers and application development recommendations. </br>
🐑💬 ➰ For saved time and complex test scenarios select a known method for communication when application development of both existing and future protocol support will make your life easier because of the gift from the explorer but not make it a landmine because they are shared resources and widely know, many people will start trying to cheat it as there are more oppotunity. </br>
🐐💬 Readble message communication by default they will extract information they are required and leave what they do not know but forward if they are ignored restriction headers fields in the communications. Once we had performed billing items counter, customer information transmission, UUID transfer for references external records from the system but there is a chance information can leak from communication messages oneway is by HTTP protocols when applications designed to work with the known system and sometimes they communication reference level you do not need to intercepts the message but by ```broadcasting duplicated``` (a technique called broadcasting duplicated ) the terminal that exists or not exists may receive search information message or required information request as they are priority action for some system. </br>

<p align="center" width="100%">
    <img width="55%" src="https://github.com/jkaewprateep/Python_and_CURL/blob/main/CURL%20command%20comm.png"> </br>
    <b> Computing command and parameters </b> </br>
</p>
</br>
</br>

<p align="center" width="100%">
    <img width="55%" src="https://github.com/jkaewprateep/Python_and_CURL/blob/main/subprocess.png"> </br>
    <b> Subprocess execution and JSON data loading </b> </br>
</p>
</br>
</br>

## Method GET ##

```
def request_GET( data, params, authen, url="https://paper-api.alpaca.markets/v2/account" ) :

    payload = dict({ });
    target_header = ["APCA-API-KEY-ID", "APCA-API-SECRET-KEY", "accept"];
    headers = dict({ "APCA-API-KEY-ID":authen.APCA_API_KEY_ID,
                        "APCA-API-SECRET-KEY":authen.APCA_API_SECRET_KEY,
                        "accept":authen.accept });

    r = None;
    if str(type(params)) in ["<class 'dict'>"] :
        r = requests.get(url, data=json.dumps(payload), headers=headers, params=params);
    else :
        r = requests.get(url, data=json.dumps(payload), headers=headers);
    
    r.headers = dict(['"{0}: {1}"'.format(k, v) for k, v in r.headers.items() if k in target_header]);
    r.body = data;
    req = r.request;

    command = "curl -X GET";
    method = req.method;
    uri = req.url;
    data = req.body;

    headers = ['"{0}: {1}"'.format(k, v) for k, v in req.headers.items() if k in target_header];
    headers = " -H " + " -H ".join(headers);
    command_tosend = command.format(method=method, headers=headers, data=data, uri=uri);
    command_tosend = command_tosend + headers + " " + uri;

    args = shlex.split(command_tosend);
    process = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate();

    result = json.loads(stdout.decode('utf-8'));

    process.stdout.close();

    return result
```

## Method POST ##

```
def request_POST( payload, params, authen, url="https://paper-api.alpaca.markets/v2/account" ) :

    target_header = ["APCA-API-KEY-ID", "APCA-API-SECRET-KEY", "accept"];
    headers = dict({ "APCA-API-KEY-ID":authen.APCA_API_KEY_ID,
                        "APCA-API-SECRET-KEY":authen.APCA_API_SECRET_KEY,
                        "accept":authen.accept });
    r = requests.post(url, data=payload, headers=headers);
    r.headers = dict(['"{0}: {1}"'.format(k, v) for k, v in r.headers.items() if k in target_header]);
    req = r.request;

    command = "curl -X POST";
    method = req.method;
    uri = req.url;

    headers = ['"{0}: {1}"'.format(k, v) for k, v in req.headers.items() if k in target_header];
    headers = " -H " + " -H ".join(headers);
    data = " -d '" + json.dumps(payload) + "'";
    command_tosend = command.format(method=method, headers=headers, data=payload, uri=uri);
    command_tosend = command_tosend + headers + data + " " + uri;

    args = shlex.split(command_tosend);
    process = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate();

    result = json.loads(stdout.decode('utf-8'));

    process.stdout.close();

    return result;
```

## Method DELETE ##

```
def request_DELETE( authen, url="https://paper-api.alpaca.markets/v2/orders" ) :
    # Attempts to cancel an Open Order. If the order is no longer cancelable, 
    # the request will be rejected with status 422; otherwise accepted with return status 204.

    target_header = ["APCA-API-KEY-ID", "APCA-API-SECRET-KEY", "accept"];
    headers = dict({ "APCA-API-KEY-ID":authen.APCA_API_KEY_ID,
                        "APCA-API-SECRET-KEY":authen.APCA_API_SECRET_KEY,
                        "accept":authen.accept });

    r = requests.delete(url, headers=headers);

    r.headers = dict(['"{0}: {1}"'.format(k, v) for k, v in r.headers.items() if k in target_header]);
    req = r.request;

    command = "curl -X DELETE";
    method = req.method;
    uri = req.url;
    data = "";

    headers = ['"{0}: {1}"'.format(k, v) for k, v in req.headers.items() if k in target_header];
    headers = " -H " + " -H ".join(headers);
    command_tosend = command.format(method=method, headers=headers, data=data, uri=uri);
    command_tosend = command_tosend + headers + " " + uri;

    print( "command_tosend: ", command_tosend )

    args = shlex.split(command_tosend);
    process = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate();

    process.stdout.close();

    result = None;
    try : 
        result = json.loads(stdout.decode('utf-8'));
    except TimeoutError :
        print( TimeoutError.__str__ );
    except BufferError :
        print( BufferError.__str__ );
    except RuntimeError :
        print( RuntimeError.__str__ );
    except :
        print( Exception );

    return result
```

## Method PATCH ##

```
def request_PATCH( payload, params, authen, url="https://paper-api.alpaca.markets/v2/account" ) :

    target_header = ["APCA-API-KEY-ID", "APCA-API-SECRET-KEY", "accept"];
    headers = dict({ "APCA-API-KEY-ID":authen.APCA_API_KEY_ID,
                        "APCA-API-SECRET-KEY":authen.APCA_API_SECRET_KEY,
                        "accept":authen.accept });

    r = requests.post(url, data=payload, headers=headers);
    r.headers = dict(['"{0}: {1}"'.format(k, v) for k, v in r.headers.items() if k in target_header]);
    req = r.request;

    command = "curl -X PATCH";
    method = req.method;
    uri = req.url;

    headers = ['"{0}: {1}"'.format(k, v) for k, v in req.headers.items() if k in target_header];
    headers = " -H " + " -H ".join(headers);
    data = " -d '" + json.dumps(payload) + "'";
    command_tosend = command.format(method=method, headers=headers, data=payload, uri=uri);
    command_tosend = command_tosend + headers + data + " " + uri;

    args = shlex.split(command_tosend);
    process = subprocess.Popen(args, shell=False, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
    stdout, stderr = process.communicate();

    result = json.loads(stdout.decode('utf-8'));

    process.stdout.close();

    return result;
```
