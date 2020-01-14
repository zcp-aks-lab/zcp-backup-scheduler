# zcp-backup-scheduler

* ### Azure account 입력
backup하는 snapshot을 생성할 때 사용할 Azure account를 secret에 base64로 encoding해서 입력
  * zcp-block-storage-backup-secret.yaml
   Change 부분에 삽입
```
$ vi zcp-block-storage-backup-secret.yaml
  ...
  azureID:    # Change
  azurePWD:    # Change
```


* ### Logging 노드가 1대인 경우에는 아래 내용 삭제
3대인 경우에는 수정할 것이 없음
  * zcp-block-storage-backup-cronjob.yaml
    containers - env 하위 ES_DATA_1, ES_DATA_2 부분 삭제
    ```
    $ vi zcp-block-storage-backup-cronjob.yaml
    ...
            - name: ES_DATA_1
              value: elasticsearch-data-elasticsearch-data-1
            - name: ES_DATA_2
              value: elasticsearch-data-elasticsearch-data-2
    ...

    ```

  * zcp-block-storage-backup-configmap.yaml
    containers - env 하위 ES_DATA_1, ES_DATA_2 부분 삭제
    ```
    $ vi zcp-block-storage-backup-cronjob.yaml
      PV List하위의 $ES_DATA_1, $ES_DATA_2를 array에 추가하는 부분 삭제
    ...
    ########################## PV List ##########################
    ...
    PV_LIST[12]="$ES_DATA_1"
    PV_LIST[13]="$ES_DATA_2"
    ...

    ```

