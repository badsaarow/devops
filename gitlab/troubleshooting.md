# GitLab

## Naver Cloud DB postgresql version

<https://guide.ncloud-docs.com/docs/clouddbforpostgresql-releasenote>

- not supported 14

```text
gitlab    |     ---- Begin output of "bash"  ----
gitlab    |     STDOUT: ██     ██  █████  ██████  ███    ██ ██ ███    ██  ██████ 
gitlab    |               ██     ██ ██   ██ ██   ██ ████   ██ ██ ████   ██ ██      
gitlab    |               ██  █  ██ ███████ ██████  ██ ██  ██ ██ ██ ██  ██ ██   ███ 
gitlab    |               ██ ███ ██ ██   ██ ██   ██ ██  ██ ██ ██ ██  ██ ██ ██    ██ 
gitlab    |                ███ ███  ██   ██ ██   ██ ██   ████ ██ ██   ████  ██████  
gitlab    |     
gitlab    |     ******************************************************************************
gitlab    |       You are using PostgreSQL 13.15 for the main database, but this version of GitLab requires PostgreSQL >= 14.
gitlab    |       
gitlab    |       Please upgrade your environment to a supported PostgreSQL version. See
gitlab    |       https://docs.gitlab.com/ee/install/requirements.html#database for details.
gitlab    |     ******************************************************************************

          ██     ██  █████  ██████  ███    ██ ██ ███    ██  ██████ 
          ██     ██ ██   ██ ██   ██ ████   ██ ██ ████   ██ ██      
          ██  █  ██ ███████ ██████  ██ ██  ██ ██ ██ ██  ██ ██   ███ 
          ██ ███ ██ ██   ██ ██   ██ ██  ██ ██ ██ ██  ██ ██ ██    ██ 
           ███ ███  ██   ██ ██   ██ ██   ████ ██ ██   ████  ██████  

******************************************************************************
  You are using PostgreSQL 13.15 for the ci database, but this version of GitLab requires PostgreSQL >= 14.
  
  Please upgrade your environment to a supported PostgreSQL version. See
  https://docs.gitlab.com/ee/install/requirements.html#database for details.
******************************************************************************
Running db:schema:load rake task
psql:/opt/gitlab/embedded/service/gitlab-rails/db/structure.sql:9: ERROR:  no schema has been selected to create in
rake aborted!
failed to execute:
psql --set ON_ERROR_STOP=1 --quiet --no-psqlrc --output /dev/null --file /opt/gitlab/embedded/service/gitlab-rails/db/structure.sql --single-transaction gitlab
```

## gitlab-runner

```text
gitlab-runner    | Runtime platform                                    arch=amd64 os=linux pid=7 revision=12030cf4 version=17.5.3
gitlab-runner    | Starting multi-runner from /etc/gitlab-runner/config.toml...  builds=0 max_builds=0
gitlab-runner    | Running in system-mode.                            
gitlab-runner    |                                                    
gitlab-runner    | Created missing unique system ID                    system_id=r_8qm1G6HgR2ZO
gitlab-runner    | Configuration loaded                                builds=0 max_builds=1
gitlab-runner    | listen_address not defined, metrics & debug endpoints disabled  builds=0 max_builds=1
gitlab-runner    | [session_server].listen_address not defined, session endpoints disabled  builds=0 max_builds=1
gitlab-runner    | Initializing executor providers                     builds=0 max_builds=1
gitlab-runner    | ERROR: Failed to load config stat /etc/gitlab-runner/config.toml: no such file or directory  builds=0 max_builds=1
gitlab-runner    | ERROR: Failed to load config stat /etc/gitlab-runner/config.toml: no such file or directory  builds=0 max_builds=1
```
