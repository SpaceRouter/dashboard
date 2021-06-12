# PROMETHEUS dashboard

PROMETHEUS monitoring software used to gather data to the OpenGate Admin Dashboard

Run:
----
    docker-compose up

Query sample :
---------

CPU Usage for Linux

	#Average
	100 - (avg by (instance) (irate(node_cpu_seconds_total{job="nodeexporter",mode="idle"}[5m])) * 100)

	#Minimum
	100 - (max by (instance) (irate(node_cpu_seconds_total{job="nodeexporter",mode="idle"}[5m])) * 100)

	#Maximum
	100 - (min by (instance) (irate(node_cpu_seconds_total{job="nodeexporter",mode="idle"}[5m]))

Memory Usage for Linux

	#Avarage:
	100 * (1 - ((avg_over_time(node_memory_MemFree_bytes{job=~"nodeexporter"}[30d]) + avg_over_time(node_memory_Cached_bytes{job=~"nodeexporter"}[30d]) + avg_over_time(node_memory_Buffers_bytes{job=~"nodeexporter"}[30d])) / avg_over_time(node_memory_MemTotal_bytes{job=~"nodeexporter"}[30d])))

	#Maximum:
	100 * (1 - ((min_over_time(node_memory_MemFree_bytes{job=~"nodeexporter"}[30d]) + min_over_time(node_memory_Cached_bytes{job=~"nodeexporter"}[30d]) + min_over_time(node_memory_Buffers_bytes{job=~"nodeexporter"}[30d])) / min_over_time(node_memory_MemTotal_bytes{job=~"nodeexporter"}[30d])))

	#Minimum
	100 * (1 - ((max_over_time(node_memory_MemFree_bytes{job=~"nodeexporter"}[30d]) + max_over_time(node_memory_Cached_bytes{job=~"nodeexporter"}[30d]) + max_over_time(node_memory_Buffers_bytes{job=~"nodeexporter"}[30d])) / max_over_time(node_memory_MemTotal_bytes{job=~"nodeexporter"}[30d])))
