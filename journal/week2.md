# Week 2 — Distributed Tracing

### HoneyComb Set Up

- Create an Environment of `AWS-Bootcamp-2023` in honeycomb and copy your API KEY
- Open Gitpod and set Environment variable

```
export HONEYCOMB_API_KEY="YOUR_API_KEY"
gp env HONEYCOMB_API_KEY="YOUR_API_KEY"
```

- Make sure not to give any spaces above as they will also considered as part of variable
- Open docker_compose.yml file in backend and add OTEL things under environment variables section

```
OTEL_SERVICE_NAME: "backend-flask"
OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
```

- Once we completed setting up Environmental Variables, we now move to requirements file in Backend folder and paste opentelemtry installations

```
opentelemetry-api 
opentelemetry-sdk 
opentelemetry-exporter-otlp-proto-http 
opentelemetry-instrumentation-flask 
opentelemetry-instrumentation-requests
```

-Install requiremts through CLI by running `pip install -r requirements.txt`
- Now as part of Initialization, Open App.py and add below contents

To the `app.py`

```
from opentelemetry import trace
from opentelemetry.instrumentation.flask import FlaskInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
```

```
# Initialize tracing and an exporter that can send data to Honeycomb
provider = TracerProvider()
processor = BatchSpanProcessor(OTLPSpanExporter())
provider.add_span_processor(processor)
trace.set_tracer_provider(provider)
tracer = trace.get_tracer(__name__)
```

```
# Initialize automatic instrumentation with Flask
app = Flask(__name__)
FlaskInstrumentor().instrument_app(app)
RequestsInstrumentor().instrument()
```

- Once you added above things, Push the changes into Github
- Check whether the the HONEYCOMB_API_KEY is set. If not make sure it to set it, else our docker won't be sending data to Honeycomb.
- Not sure why my docker is not sending any data into honey comb though everything is in place.I have commented out the Dynamo DB and Postgress code in Docker Compose file and it somehow sent data to HoneyComb.

[Honeycomb_Config_Commit](https://github.com/NiteeshKumar31/aws-bootcamp-cruddur-2023/commit/03e599c75433f0597c7c4a8c0369306d2be5339f)

###### Creating A Tracer for Home Activities

Open home_activities.py and add belwo code from [opentelemetry_python](https://docs.honeycomb.io/getting-data-in/opentelemetry/python/) and follow steps from creating spans

```
from opentelemetry import trace

tracer = trace.get_tracer("home.activities")

````

- Add the below code inside run function and check on the indentations

```
with tracer.start_as_current_span("home-activities-mock-data"):
```


- Add below code inside with tracer statement

```
span = trace.get_current_span()
span.set_attribute("user.id", user.id())
```

[Tracer_Commit](https://github.com/NiteeshKumar31/aws-bootcamp-cruddur-2023/commit/3e09ad4d439165188dc42d29e84b3c55116ce910)



