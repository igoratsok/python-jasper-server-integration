#  Python JasperServer Integration
Python JSIntegration is a python module that quickly integrates node.js to Jasper Server and retrieves the bytes data of the exported report.

# Usage
Usage is quite simple:
```python 
#!/usr/bin/python
from jsintegration.JasperServerIntegration import JasperServerIntegration
from io import BytesIO

obj = JasperServerIntegration(
    'http://localhost:8080/jasperserver', # URL of the Jasper Server
  'reports/aluno_escola_filtro',         # Path to the Report Unit
  'pdf',                                  # Export type
  'jasperadmin',                          # User
  'jasperadmin',                          # Password
  {"P_ID_ALUNO" :  1}                     # Optional parameters
)

# get the bytes from the generated report
try:
  report = obj.execute()

  # create a BytesIO from the bytes from the report
  report_bytesio = BytesIO(report)

  # save file to report.pdf
  with open("report.pdf", "wb") as f:
      f.write(report_bytesio.getbuffer())
except:
  print('Error ' + obj.error_code + ': ' + obj.error_message)
```
