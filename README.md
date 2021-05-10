# Elastic stack (ELK--filebeat) on Docker

[![Elastic Stack version](https://img.shields.io/badge/Elastic%20Stack-7.12.1-00bfb3?style=flat&logo=elastic-stack)](https://www.elastic.co/blog/category/releases)
[![Build Status](https://github.com/deviantony/docker-elk/workflows/CI/badge.svg?branch=main)](https://github.com/deviantony/docker-elk/actions?query=workflow%3ACI+branch%3Amain)
[![Join the chat at https://gitter.im/deviantony/docker-elk](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/deviantony/docker-elk?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Docker 및 Docker Compose를 사용하여 최신버전의 [Elastic stack][elk-stack] 을 사용합니다.

Elasticsearch와 Kibana의 능력은 검색/집계 기능을 사용하여 데이터를 분석할 수 있게 합니다.

* : information_source :이 스택을 지원하는 Docker 이미지에는 [유료 기능] [유료 기능]과 함께 [X-Pack] [xpack]이 포함됩니다.
기본적으로 비활성화됩니다  ** [trial license][trial-license]는 30 일 ** 동안 유효합니다. 이 라이센스가 만료 된 후에도 무료 기능을 계속 사용할 수 있습니다.


이 DockerImage는 Elatic의 공식 Docker 이미지를 기반으로 합니다.

* [Elasticsearch](https://github.com/elastic/elasticsearch/tree/master/distribution/docker)
* [Logstash](https://github.com/elastic/logstash/tree/master/docker)
* [Kibana](https://github.com/elastic/kibana/tree/master/src/dev/build/tasks/os_packages/docker_generator)

---

## Contents

1. [Requirements](#requirements)
   * [Host setup](#host-setup)
   * [Environment setup](#environment-setup)
   * [Initial Setting](#Initial-setting)
   
1. [Usage](#usage)
   * [Version selection](#version-selection)
   * [Bringing up the stack](#bringing-up-the-stack)

## Requirements
   docker version >= 20.10.6

## Host setup
기본적으로 스택은 다음 포트를 사용합니다.

* 5044: Logstash Beats input
* 5000: Logstash TCP input
* 9600: Logstash monitoring API
* 9200: Elasticsearch HTTP
* 9300: Elasticsearch TCP transport
* 5601: Kibana

## Environment setup
   
* .env파일에 환경변수를 작성합니다.
*  이 예제에서 logstash는 mysql과 통신합니다.
* .env파일을 작성하세요. 기본은 localhost입니다. 원격지를 지정하려면 다음과 같이 입력하세요 HOST=12.345.678.901

## Initial setting

* 처음에 ./envs/elasticsearch/config, ./envs/kibana/config, ./envs/filebeat/config, ./envs/logstash/config폴더에 *.yml 이나 *.conf파일을 원하는대로 수정하세요.

## Usage

### Version selection

이 repository는 최신 버전의 Elastic 스택을 유지합니다. `main` branch는 현재(7.x)입니다.

다른 버전의 핵심 Elastic 구성 요소를 사용하려면`.env` 파일에서 버전 번호를 변경하면됩니다. 만약
기존 스택을 업그레이드하는 경우 다음 섹션의 참고 사항을주의 깊게 읽으십시오.

** : 경고 : 각 개별 구성 요소에 대한 [공식 업그레이드 지침] [업그레이드]에 항상주의하십시오.
스택 업그레이드를 수행합니다. **

이전 주 버전도 별도의 brances에서 지원됩니다.

* [`release-6.x`] (https://github.com/deviantony/docker-elk/tree/release-6.x) : 6.x 시리즈
* [`release-5.x`] (https://github.com/deviantony/docker-elk/tree/release-5.x) : 5.x 시리즈 (End-Of-Life)


### Bringing up the stack

스택을 실행할 Docker 호스트에이 저장소를 복제한 다음 Docker Compose를 사용하여 로컬에서 서비스를 시작합니다.

```console
$ docker-compose up
```

위 명령어에 `-d` 플래그를 추가하여 모든 서비스를 백그라운드 (detached 모드)에서 실행할 수 있습니다.

** : 경고 : 분기를 전환하거나 업데이트 할 때마다 `docker-compose build`로 스택 이미지를 다시 빌드해야합니다.
이미 존재하는 스택의 버전. **

처음으로 스택을 시작하는 경우 아래 섹션을주의 깊게 읽으십시오.

[elk-stack]: https://www.elastic.co/what-is/elk-stack
[xpack]: https://www.elastic.co/what-is/open-x-pack
[paid-features]: https://www.elastic.co/subscriptions
[trial-license]: https://www.elastic.co/guide/en/elasticsearch/reference/current/license-settings.html

[elastdocker]: https://github.com/sherifabdlnaby/elastdocker

[linux-postinstall]: https://docs.docker.com/install/linux/linux-postinstall/

[booststap-checks]: https://www.elastic.co/guide/en/elasticsearch/reference/current/bootstrap-checks.html
[es-sys-config]: https://www.elastic.co/guide/en/elasticsearch/reference/current/system-config.html

[win-shareddrives]: https://docs.docker.com/docker-for-windows/#shared-drives
[mac-mounts]: https://docs.docker.com/docker-for-mac/osxfs/

[builtin-users]: https://www.elastic.co/guide/en/elasticsearch/reference/current/built-in-users.html
[ls-security]: https://www.elastic.co/guide/en/logstash/current/ls-security.html
[sec-tutorial]: https://www.elastic.co/guide/en/elasticsearch/reference/current/security-getting-started.html

[connect-kibana]: https://www.elastic.co/guide/en/kibana/current/connect-to-elasticsearch.html
[index-pattern]: https://www.elastic.co/guide/en/kibana/current/index-patterns.html

[config-es]: ./elasticsearch/config/elasticsearch.yml
[config-kbn]: ./kibana/config/kibana.yml
[config-ls]: ./logstash/config/logstash.yml

[es-docker]: https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html
[kbn-docker]: https://www.elastic.co/guide/en/kibana/current/docker.html
[ls-docker]: https://www.elastic.co/guide/en/logstash/current/docker-config.html

[log4j-props]: https://github.com/elastic/logstash/tree/7.6/docker/data/logstash/config
[esuser]: https://github.com/elastic/elasticsearch/blob/7.6/distribution/docker/src/docker/Dockerfile#L23-L24

[upgrade]: https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-upgrade.html

[swarm-mode]: https://docs.docker.com/engine/swarm/
