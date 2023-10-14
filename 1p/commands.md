# Helpful Commmands

## Get PAT from vault

```
function get

op item get pat-github \
  --vault zfce \
  --format json|
  jq -r '.fields[] | select(.id == "credential") | .value | select( . != null )'
  
  
op --account z0 read op://zfce/pat-github/credential  
```

```
op --account z0 read op://zfce/projects-github/refnotes
```