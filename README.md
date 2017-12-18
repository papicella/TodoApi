## ToDo API for DOTNET 2.0

This demo is for Pivotal Cloud Foundry and requires dotnet 2.0 built as a Web API using ASP .NET Core  

### Steps

- Clone as follows

```
$ git clone https://github.com/papicella/TodoApi.git
```

- Change to "TodoApi" directory

```
$ cd TodoApi
```

- Use the dotnet CLI to restore the NuGet references used by the application

```
$ dotnet restore 
```

- Publish the application to get it ready to push to Cloud Foundry.

Note: we are specifying the runtime by using -r ubuntu.14.04-x64 during our publish command as we will be pushing this application to a Linux cell on Cloud Foundry

```
$ dotnet publish --output ./publish --configuration Release --runtime ubuntu.14.04-x64
```

- Push to Pivota Cloud Foundry

```
$ cf push 
```

You can see from the manifest.yml we are publishing from the "./publish" directory we created above

```
---
applications:
- name: dotnet-webapi
  memory: 512M
  instances: 1
  random-route: true
  path: ./publish
  env:
      ASPNETCORE_ENVIRONMENT: Development
```

- Once deployed verify route to application as shown below

```
pasapicella@pas-macbook:~/temp/TodoApi$ cf apps
Getting apps in org pivot-papicella / space dotnet as papicella@pivotal.io...
OK

name            requested state   instances   memory   disk   urls
dotnet-webapi   started           1/1         512M     1G     dotnet-webapi-isandrous-puzzolana.pcfbeta.io
```

- Access API endpoint as follows showing the current TODO items

```
pasapicella@pas-macbook:~/temp/TodoApi$ http https://dotnet-webapi-isandrous-puzzolana.pcfbeta.io/api/todo
HTTP/1.1 200 OK
Content-Length: 230
Content-Type: application/json; charset=utf-8
Date: Mon, 18 Dec 2017 11:46:00 GMT
Server: Kestrel
X-Vcap-Request-Id: 92d76f6b-afe0-4c43-7c28-cf2cf0f93af8

[
    {
        "id": 1,
        "isComplete": true,
        "name": "Do the washing"
    },
    {
        "id": 2,
        "isComplete": true,
        "name": "Take dog for a walk"
    },
    {
        "id": 3,
        "isComplete": false,
        "name": "Buy MSFT stock"
    },
    {
        "id": 4,
        "isComplete": false,
        "name": "Watch the AFL grand final replay"
    }
]
```

<hr />
Pas Apicella [papicella at pivotal.io] is a Senior Platform Architect at Pivotal Australia 

