# dmfcta
Docker container for monitoring file changes to do action

This is an example `compose.yml` to use this tool, the feature is like hot-reload
```yaml
services:
  app:
    image: ghcr.io/vleedev/dmfcta:main
    volumes:
      - ./test/sample:/app/test/sample:ro
    environment:
      # Declare keys to indicate app to take envs
      # If we don't set, the default one will be used
      DMFCTA_ACTION_KEY: ACTION
      DMFCTA_CRITERIA_KEY: CRITERIA
      DMFCTA_SHELL_KEY: SHELL
      DMFCTA_TIMEOUT_KEY: TIMEOUT
      # Declare 0
      # default SHELL and TIMEOUT
      CRITERIA_0: /app/test/sample
      ACTION_0: echo test1
      # Declare 1, the action is the same with 0
      # default SHELL and TIMEOUT
      CRITERIA_1: /app/test/sample/test1.txt
      ACTION_1: echo test1
      # Declare 2
      # default SHELL and TIMEOUT
      CRITERIA_2: /app/test/sample/test2.txt
      ACTION_2: echo test2
      # Declare 3, wrong shell
      CRITERIA_3: /app/test/sample/test3.txt
      ACTION_3: echo test3
      SHELL_3: bash1
      # Declare 4, over the timeout
      # default SHELL
      CRITERIA_4: /app/test/sample/test4.txt
      ACTION_4: echo test4; sleep 10; echo ok
      TIMEOUT_4: 2
```