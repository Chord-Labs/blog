kill
```bash
  ps -ef | grep '****' | grep '****' | cut -c 9-15 | xargs kill -15
  
  ps -ef | grep 'python38' | grep 'run_mm.py' | cut -c 9-15 | xargs kill -15
```

Mac
```
ps -ef | grep 'Python' | awk '{print $2}' | xargs kill -15
```
