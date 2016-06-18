################################################################################
#  Licensed to the Apache Software Foundation (ASF) under one
#  or more contributor license agreements.  See the NOTICE file
#  distributed with this work for additional information
#  regarding copyright ownership.  The ASF licenses this file
#  to you under the Apache License, Version 2.0 (the
#  "License"); you may not use this file except in compliance
#  with the License.  You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
#  Unless required by applicable law or agreed to in writing, software
#  distributed under the License is distributed on an "AS IS" BASIS,
#  WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#  See the License for the specific language governing permissions and
# limitations under the License.
################################################################################

FROM flink

RUN curl -L https://github.com/ecesena/beam-starter/releases/download/v0.1/beam-starter-0.1.jar > /root/downloads/beam-starter-0.1.jar

RUN curl http://www.gutenberg.org/cache/epub/1128/pg1128.txt > /tmp/kinglear.txt

ADD config-flink-load-jar.sh /usr/local/flink/bin/
RUN chmod +x /usr/local/flink/bin/config-flink-load-jar.sh

#TODO load jar at image level (Flink doesn't allow this yet)
#RUN (/usr/local/flink/bin/config-flink.sh jobmanager &); \
#    sleep 10 && \
#	curl -H "Expect:" -F "jarfile=@/root/downloads/beam-starter-0.1.jar;type=application/java-archive" http://localhost:8080/jars/upload && \
#	/usr/local/flink/bin/jobmanager.sh stop

CMD ["/usr/local/flink/bin/config-flink.sh", "taskmanager"]
