# prep_process for REST job UC4 - How to set it up

> Create a new REST Job, or multiple based on the type of request and name it with a preceeding EVENT.; e.g. EVENT.REST_GET or EVENT.REST_POST...

## Configs in the REST job

### Insert below script in pre-process

```
:beginread
:  read &link,         '00', 'Override Url',,MC
:  read &conn,         '00', 'Connection object name',,MC
:  read &login,         '00', 'Login object',,MC
:  read &host,         '00', 'RA Agent',,MC
:  read &uc_eventfile,'00', 'Reply file to UC4',,M
:endread
:put_att HOST = &host
:put_att LOGIN = &login
```

### Adjust below attributes

> The override url for the REST request should be populated with the script variable _'&link'_

<img alt="A screenshot from the Web Service pane of a WebServiceREST job" src="https://raw.githubusercontent.com/vegaflare/uc4-scripts/refs/heads/main/imgs/img_override_link.PNG">


> The response file should be defined with the script variable _&uc_eventfile_

<img alt="A screenshot from the response of a WebServiceREST job" src="https://raw.githubusercontent.com/vegaflare/uc4-scripts/refs/heads/main/imgs/img_response_file.PNG">

### Here comes the examples as to how to call it using [prep_process](https://docs.automic.com/documentation/webhelp/english/ARA/11.2/AE/11.2/All%20Guides/Content/ucaafp.htm)
> In this example we just get the status if the UC4 automation engine using it's API
```
:set &hnd = prep_process("RA-REST-1", "REST_GET", "*Running*","host=RA-REST-1", "link=http://host1:8088/ae/api/v1/0007/system/health","conn=REST_TST_CONN","UC_LOGIN=LOGIN.OBJECKT")
:process &hnd
:  set &val = get_process_line(&hnd)
:  p &val
:endprocess
```

If you see closely, you will find that I am passing the name of a connection object as well. 
So, if you are not a dummy you would be correct thinking that it is not possible to change the connection objekt at runtime
Then why TH is it being used, well you see 👉👈, I'm a bit of a nerd (way past a bit). I figured out way to change it, now this is the tricky part, it can break things.

> [!WARNING]
> As I said, it made things go wrong for me. UNABLE TO MODIFY OR DELETE the RA objekt after this.
> If you don't want it, the just remove `,"conn=REST_TST_CONN"` from the prep_process parameters.

> Still wanna do it ? Brave one aren't ya'
> Okay, here's how:

* Export the RA objekt (EVENT.REST_GET in my case)
* find `<component con="1" enc="0" type="2" value="REST_TST_CONN" xmlName="restConnection"/>` in the xml file.
* replace the existing value with the new variable (this is not allowed via the AWI),
    `value="REST_TST_CONN"` to `value="&amp;conn"` because my script variable is &conn.
* Import it back, voila!


> [!TIP]
> Explore more customization knowing that all parameters you pass through prep_process are kept in the read_buffer 😉


