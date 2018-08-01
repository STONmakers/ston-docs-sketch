.. _api:

API
******************

API 목록 레퍼런스. 모든 API는 다음과 같이 호출한다. ::

   http://{ston-ip}:10040/{API}


Meta
====================================

- ``/help``
- ``/ver``
- ``/version``



설정
====================================

관리
------------------------------------
- ``/conf/reload``
- ``/conf/reloadserver``
- ``/conf/reloadvhosts``
- ``/conf/export``
- ``/conf/import``
- ``/conf/download``
- ``/conf/latest``
- ``/conf/history``
- ``/conf/restore``

열람
------------------------------------
- ``/conf/server.xml``
- ``/conf/vhosts.xml``
- ``/conf/bypass.txt``
- ``/conf/ttl.txt``
- ``/conf/expires.txt``
- ``/conf/acl.txt``
- ``/conf/headers.txt``
- ``/conf/querystring.txt``
- ``/conf/throttling.txt``
- ``/conf/postbody.txt``
- ``/conf/compression.txt``



명령어
====================================

서버운영
------------------------------------
- ``/command/restart``
- ``/command/terminate``
- ``/command/cacheclear``
- ``/command/unmount``
- ``/command/umount``
- ``/command/mount``

캐싱객체 관리
------------------------------------
- ``/command/hardpurge``
- ``/command/purge``
- ``/command/expire``
- ``/command/expireafter``

기타
------------------------------------
- ``/command/resetorigin``
- ``/command/cleanup``
- ``/command/update``
- ``/command/convertregexp``
- ``/command/encryptpassword``



모니터링
====================================

통계
------------------------------------
- ``/monitoring/average.xml``
- ``/monitoring/average.json``
- ``/monitoring/realtime.xml``
- ``/monitoring/realtime.json``
- ``/monitoring/fileinfo.json``
- ``/monitoring/hwinfo.json``
- ``/monitoring/cpuinfo.json``
- ``/monitoring/vhostslist.json``
- ``/monitoring/geoiplist.json``
- ``/monitoring/ssl.json``
- ``/monitoring/cacheresource.json``
- ``/monitoring/origin.json``
- ``/monitoring/clusterlist``


로그
------------------------------------
- ``/monitoring/logtrace/info``
- ``/monitoring/logtrace/deny``
- ``/monitoring/logtrace/sys``
- ``/monitoring/logtrace/access``
- ``/monitoring/logtrace/origin``
- ``/monitoring/logtrace/monitoring``
- ``/monitoring/logtrace/originerror``


전역 그래프
------------------------------------
- ``/graph/cpu_day.png``
- ``/graph/cpu_week.png``
- ``/graph/cpu_month.png``
- ``/graph/cpu_year.png``
- ``/graph/cpu_dash.png``
- ``/graph/stoncpu_day.png``
- ``/graph/stoncpu_week.png``
- ``/graph/stoncpu_month.png``
- ``/graph/stoncpu_year.png``
- ``/graph/stoncpu_dash.png``
- ``/graph/mem_day.png``
- ``/graph/mem_week.png``
- ``/graph/mem_month.png``
- ``/graph/mem_year.png``
- ``/graph/mem_dash.png``
- ``/graph/ssockevent_day.png``
- ``/graph/ssockevent_week.png``
- ``/graph/ssockevent_month.png``
- ``/graph/ssockevent_year.png``
- ``/graph/ssockevent_dash.png``
- ``/graph/ssockusage_day.png``
- ``/graph/ssockusage_week.png``
- ``/graph/ssockusage_month.png``
- ``/graph/ssockusage_year.png``
- ``/graph/ssockusage_dash.png``
- ``/graph/csockevent_day.png``
- ``/graph/csockevent_week.png``
- ``/graph/csockevent_month.png``
- ``/graph/csockevent_year.png``
- ``/graph/csockevent_dash.png``
- ``/graph/csockusage_day.png``
- ``/graph/csockusage_week.png``
- ``/graph/csockusage_month.png``
- ``/graph/csockusage_year.png``
- ``/graph/csockusage_dash.png``
- ``/graph/eq_day.png``
- ``/graph/eq_week.png``
- ``/graph/eq_month.png``
- ``/graph/eq_year.png``
- ``/graph/eq_dash.png``
- ``/graph/wf2w_day.png``
- ``/graph/wf2w_week.png``
- ``/graph/wf2w_month.png``
- ``/graph/wf2w_year.png``
- ``/graph/wf2w_dash.png``
- ``/graph/loadavg_day.png``
- ``/graph/loadavg_week.png``
- ``/graph/loadavg_month.png``
- ``/graph/loadavg_year.png``
- ``/graph/loadavg_dash.png``
- ``/graph/acldenied_day.png``
- ``/graph/acldenied_week.png``
- ``/graph/acldenied_month.png``
- ``/graph/acldenied_year.png``
- ``/graph/acldenied_dash.png``
- ``/graph/iowait_day.png``
- ``/graph/iowait_week.png``
- ``/graph/iowait_month.png``
- ``/graph/iowait_year.png``
- ``/graph/iowait_dash.png``
- ``/graph/tcpsocket_day.png``
- ``/graph/tcpsocket_week.png``
- ``/graph/tcpsocket_month.png``
- ``/graph/tcpsocket_year.png``
- ``/graph/tcpsocket_dash.png``
- ``/graph/urlrewrite_day.png``
- ``/graph/urlrewrite_week.png``
- ``/graph/urlrewrite_month.png``
- ``/graph/urlrewrite_year.png``
- ``/graph/urlrewrite_dash.png``



가상호스트 그래프
------------------------------------
- ``/graph/vhost/mem_day.png``
- ``/graph/vhost/mem_week.png``
- ``/graph/vhost/mem_month.png``
- ``/graph/vhost/mem_year.png``
- ``/graph/vhost/mem_dash.png``
- ``/graph/vhost/wf2d_day.png``
- ``/graph/vhost/wf2d_week.png``
- ``/graph/vhost/wf2d_month.png``
- ``/graph/vhost/wf2d_year.png``
- ``/graph/vhost/wf2d_dash.png``
- ``/graph/vhost/client_httpreq_bypass_day.png``
- ``/graph/vhost/client_httpreq_bypass_week.png``
- ``/graph/vhost/client_httpreq_bypass_month.png``
- ``/graph/vhost/client_httpreq_bypass_year.png``
- ``/graph/vhost/client_httpreq_bypass_dash.png``
- ``/graph/vhost/client_httpreq_denied_day.png``
- ``/graph/vhost/client_httpreq_denied_week.png``
- ``/graph/vhost/client_httpreq_denied_month.png``
- ``/graph/vhost/client_httpreq_denied_year.png``
- ``/graph/vhost/client_httpreq_denied_dash.png``
- ``/graph/vhost/origin_http_session_day.png``
- ``/graph/vhost/origin_http_session_week.png``
- ``/graph/vhost/origin_http_session_month.png``
- ``/graph/vhost/origin_http_session_year.png``
- ``/graph/vhost/origin_http_session_dash.png``
- ``/graph/vhost/origin_traffic_day.png``
- ``/graph/vhost/origin_traffic_week.png``
- ``/graph/vhost/origin_traffic_month.png``
- ``/graph/vhost/origin_traffic_year.png``
- ``/graph/vhost/origin_traffic_dash.png``
- ``/graph/vhost/origin_http_res_day.png``
- ``/graph/vhost/origin_http_res_week.png``
- ``/graph/vhost/origin_http_res_month.png``
- ``/graph/vhost/origin_http_res_year.png``
- ``/graph/vhost/origin_http_res_dash.png``
- ``/graph/vhost/origin_http_res_complete_day.png``
- ``/graph/vhost/origin_http_res_complete_week.png``
- ``/graph/vhost/origin_http_res_complete_month.png``
- ``/graph/vhost/origin_http_res_complete_year.png``
- ``/graph/vhost/origin_http_res_complete_dash.png``
- ``/graph/vhost/origin_http_res_detail_day.png``
- ``/graph/vhost/origin_http_res_detail_week.png``
- ``/graph/vhost/origin_http_res_detail_month.png``
- ``/graph/vhost/origin_http_res_detail_year.png``
- ``/graph/vhost/origin_http_res_detail_dash.png``
- ``/graph/vhost/origin_http_res_time1_day.png``
- ``/graph/vhost/origin_http_res_time1_week.png``
- ``/graph/vhost/origin_http_res_time1_month.png``
- ``/graph/vhost/origin_http_res_time1_year.png``
- ``/graph/vhost/origin_http_res_time1_dash.png``
- ``/graph/vhost/origin_http_res_time2_day.png``
- ``/graph/vhost/origin_http_res_time2_week.png``
- ``/graph/vhost/origin_http_res_time2_month.png``
- ``/graph/vhost/origin_http_res_time2_year.png``
- ``/graph/vhost/origin_http_res_time2_dash.png``
- ``/graph/vhost/client_http_session_day.png``
- ``/graph/vhost/client_http_session_week.png``
- ``/graph/vhost/client_http_session_month.png``
- ``/graph/vhost/client_http_session_year.png``
- ``/graph/vhost/client_http_session_dash.png``
- ``/graph/vhost/client_traffic_day.png``
- ``/graph/vhost/client_traffic_week.png``
- ``/graph/vhost/client_traffic_month.png``
- ``/graph/vhost/client_traffic_year.png``
- ``/graph/vhost/client_traffic_dash.png``
- ``/graph/vhost/client_http_res_day.png``
- ``/graph/vhost/client_http_res_week.png``
- ``/graph/vhost/client_http_res_month.png``
- ``/graph/vhost/client_http_res_year.png``
- ``/graph/vhost/client_http_res_dash.png``
- ``/graph/vhost/client_http_res_complete_day.png``
- ``/graph/vhost/client_http_res_complete_week.png``
- ``/graph/vhost/client_http_res_complete_month.png``
- ``/graph/vhost/client_http_res_complete_year.png``
- ``/graph/vhost/client_http_res_complete_dash.png``
- ``/graph/vhost/client_http_res_detail_day.png``
- ``/graph/vhost/client_http_res_detail_week.png``
- ``/graph/vhost/client_http_res_detail_month.png``
- ``/graph/vhost/client_http_res_detail_year.png``
- ``/graph/vhost/client_http_res_detail_dash.png``
- ``/graph/vhost/client_http_res_time1_day.png``
- ``/graph/vhost/client_http_res_time1_week.png``
- ``/graph/vhost/client_http_res_time1_month.png``
- ``/graph/vhost/client_http_res_time1_year.png``
- ``/graph/vhost/client_http_res_time1_dash.png``
- ``/graph/vhost/client_http_res_time2_day.png``
- ``/graph/vhost/client_http_res_time2_week.png``
- ``/graph/vhost/client_http_res_time2_month.png``
- ``/graph/vhost/client_http_res_time2_year.png``
- ``/graph/vhost/client_http_res_time2_dash.png``
- ``/graph/vhost/client_http_res_hit_day.png``
- ``/graph/vhost/client_http_res_hit_week.png``
- ``/graph/vhost/client_http_res_hit_month.png``
- ``/graph/vhost/client_http_res_hit_year.png``
- ``/graph/vhost/client_http_res_hit_dash.png``
- ``/graph/vhost/client_traffic_ssl_day.png``
- ``/graph/vhost/client_traffic_ssl_week.png``
- ``/graph/vhost/client_traffic_ssl_month.png``
- ``/graph/vhost/client_traffic_ssl_year.png``
- ``/graph/vhost/client_traffic_ssl_dash.png``
- ``/graph/vhost/hitratio_day.png``
- ``/graph/vhost/hitratio_week.png``
- ``/graph/vhost/hitratio_month.png``
- ``/graph/vhost/hitratio_year.png``
- ``/graph/vhost/hitratio_dash.png``
- ``/graph/vhost/filecount_day.png``
- ``/graph/vhost/filecount_week.png``
- ``/graph/vhost/filecount_month.png``
- ``/graph/vhost/filecount_year.png``
- ``/graph/vhost/filecount_dash.png``

