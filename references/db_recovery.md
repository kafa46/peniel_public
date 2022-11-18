# 서버를 복구하는 방법

## Sqlite 삭제 및 초기화

- name.db 삭제
- migratations 폴더 삭제 (필요하다면 삭제 전 백업 하기)
- 데이터베이스 초기화
    ```bash
    $ flask db init
    $ export FLASK_APP=peniel
    $ export FLASK_DEBUG=True
    $ flask db migrate
    ```

## `.sql` 파일 업로드

    ````bash
    $ sqlite3 newDBname.db # 새로 생성한 DB 파일명 (예: peniel.db)
    $ sqlite> .read data.sql  # .sql 파일 이름 
    ````

## 이후 `migration`, `upgrade`를 통해 DB 유지보수


