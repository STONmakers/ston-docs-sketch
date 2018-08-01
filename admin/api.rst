﻿.. _api:

API
******************

API 목록 레퍼런스

Meta
====================================

- /help
- /ver
- /version



설정
====================================

- /conf/reload", OnConfReloadAll)
- /conf/reloadall", OnConfReloadAll)
- /conf/reloadserver", OnConfReloadAll)
- /conf/reloadvhosts", OnConfReloadAll)
- /conf/server.xml", OnConfServerXml)
- /conf/vhosts.xml", OnConfVhostsXml)
- /conf/bypass.txt", OnConfBypassTxt)
- /conf/ttl.txt", OnConfTTLTxt)
- /conf/expires.txt", OnConfExpiresTxt)
- /conf/acl.txt", OnConfAclTxt)
- /conf/headers.txt", OnConfHeadersTxt)
- /conf/querystring.txt", OnConfQueryStringTxt)
- /conf/throttling.txt", OnConfThrottlingTxt)
- /conf/postbody.txt", OnConfPostBodyTxt)
- /conf/compression.txt", OnConfCompressionTxt)
- /conf/export", OnConfExport)
- /conf/import", OnConfImport)
- /conf/history", OnConfHistory)
- /conf/restore", OnConfRestore)
- /conf/download", OnConfDownload)
- /conf/latest", OnConfLatest)	



명령어
====================================

- /command/hardpurge
- /command/purge
- /command/expire
- /command/expireafter
- /command/restart
- /command/terminate
- /command/cacheclear
- /command/unmount
- /command/umount
- /command/mount
- /command/resetorigin
- /command/cleanup
- /command/update
- /command/convertregexp
- /command/encryptpassword



모니터링
====================================

통계
------------------------------------
- /monitoring/average.xml
- /monitoring/average.json
- /monitoring/realtime.xml
- /monitoring/realtime.json
- /monitoring/fileinfo.json
- /monitoring/hwinfo.json
- /monitoring/cpuinfo.json
- /monitoring/vhostslist.json
- /monitoring/geoiplist.json
- /monitoring/ssl.json
- /monitoring/cacheresource.json
- /monitoring/origin.json
- /monitoring/clusterlist


로그
------------------------------------
- /monitoring/logtrace/info
- /monitoring/logtrace/deny
- /monitoring/logtrace/sys
- /monitoring/logtrace/access
- /monitoring/logtrace/origin
- /monitoring/logtrace/monitoring
- /monitoring/logtrace/originerror


전역 그래프
------------------------------------
- /graph/cpu_day.png", OnGraphGlobalCpuDay)
- /graph/cpu_week.png", OnGraphGlobalCpuWeek)
- /graph/cpu_month.png", OnGraphGlobalCpuMonth)
- /graph/cpu_year.png", OnGraphGlobalCpuYear)
- /graph/cpu_dash.png", OnGraphGlobalCpuDash)
- /graph/stoncpu_day.png", OnGraphGlobalStonCpuDay)
- /graph/stoncpu_week.png", OnGraphGlobalStonCpuWeek)
- /graph/stoncpu_month.png", OnGraphGlobalStonCpuMonth)
- /graph/stoncpu_year.png", OnGraphGlobalStonCpuYear)
- /graph/stoncpu_dash.png", OnGraphGlobalStonCpuDash)
- /graph/mem_day.png", OnGraphGlobalMemDay)
- /graph/mem_week.png",OnGraphGlobalMemWeek)
- /graph/mem_month.png", OnGraphGlobalMemMonth)
- /graph/mem_year.png",OnGraphGlobalMemYear)
- /graph/mem_dash.png", OnGraphGlobalMemDash)
- /graph/ssockevent_day.png", OnGraphGlobalServerSocketEventDay)
- /graph/ssockevent_week.png",OnGraphGlobalServerSocketEventWeek)
- /graph/ssockevent_month.png", OnGraphGlobalServerSocketEventMonth)
- /graph/ssockevent_year.png",OnGraphGlobalServerSocketEventYear)
- /graph/ssockevent_dash.png", OnGraphGlobalServerSocketEventDash)
- /graph/ssockusage_day.png", OnGraphGlobalServerSocketUsageDay)
- /graph/ssockusage_week.png",OnGraphGlobalServerSocketUsageWeek)
- /graph/ssockusage_month.png", OnGraphGlobalServerSocketUsageMonth)
- /graph/ssockusage_year.png",OnGraphGlobalServerSocketUsageYear)
- /graph/ssockusage_dash.png", OnGraphGlobalServerSocketUsageDash)
- /graph/csockevent_day.png", OnGraphGlobalClientSocketEventDay)
- /graph/csockevent_week.png",OnGraphGlobalClientSocketEventWeek)
- /graph/csockevent_month.png", OnGraphGlobalClientSocketEventMonth)
- /graph/csockevent_year.png",OnGraphGlobalClientSocketEventYear)
- /graph/csockevent_dash.png", OnGraphGlobalClientSocketEventDash)
- /graph/csockusage_day.png", OnGraphGlobalClientSocketUsageDay)
- /graph/csockusage_week.png",OnGraphGlobalClientSocketUsageWeek)
- /graph/csockusage_month.png", OnGraphGlobalClientSocketUsageMonth)
- /graph/csockusage_year.png",OnGraphGlobalClientSocketUsageYear)
- /graph/csockusage_dash.png", OnGraphGlobalClientSocketUsageDash)
- /graph/eq_day.png", OnGraphGlobalEQDay)
- /graph/eq_week.png",OnGraphGlobalEQWeek)
- /graph/eq_month.png", OnGraphGlobalEQMonth)
- /graph/eq_year.png",OnGraphGlobalEQYear)
- /graph/eq_dash.png", OnGraphGlobalEQDash)
- /graph/wf2w_day.png", OnGraphGlobalWaitingFiles2WriteDay)
- /graph/wf2w_week.png",OnGraphGlobalWaitingFiles2WriteWeek)
- /graph/wf2w_month.png", OnGraphGlobalWaitingFiles2WriteMonth)
- /graph/wf2w_year.png",OnGraphGlobalWaitingFiles2WriteYear)
- /graph/wf2w_dash.png", OnGraphGlobalWaitingFiles2WriteDash)
- /graph/loadavg_day.png", OnGraphGlobalLoadAverageDay)
- /graph/loadavg_week.png", OnGraphGlobalLoadAverageWeek)
- /graph/loadavg_month.png", OnGraphGlobalLoadAverageMonth)
- /graph/loadavg_year.png", OnGraphGlobalLoadAverageYear)
- /graph/loadavg_dash.png", OnGraphGlobalLoadAverageDash)
- /graph/acldenied_day.png", OnGraphGlobalAclDeniedDay)
- /graph/acldenied_week.png", OnGraphGlobalAclDeniedWeek)
- /graph/acldenied_month.png", OnGraphGlobalAclDeniedMonth)
- /graph/acldenied_year.png", OnGraphGlobalAclDeniedYear)
- /graph/acldenied_dash.png", OnGraphGlobalAclDeniedDash)
- /graph/iowait_day.png", OnGraphGlobalIOWaitDay)
- /graph/iowait_week.png", OnGraphGlobalIOWaitWeek)
- /graph/iowait_month.png", OnGraphGlobalIOWaitMonth)
- /graph/iowait_year.png", OnGraphGlobalIOWaitYear)
- /graph/iowait_dash.png", OnGraphGlobalIOWaitDash)
- /graph/tcpsocket_day.png", OnGraphGlobalTCPSocketDay)
- /graph/tcpsocket_week.png", OnGraphGlobalTCPSocketWeek)
- /graph/tcpsocket_month.png", OnGraphGlobalTCPSocketMonth)
- /graph/tcpsocket_year.png", OnGraphGlobalTCPSocketYear)
- /graph/tcpsocket_dash.png", OnGraphGlobalTCPSocketDash)
- /graph/urlrewrite_day.png", OnGraphGlobalUrlRewriteDay)
- /graph/urlrewrite_week.png", OnGraphGlobalUrlRewriteWeek)
- /graph/urlrewrite_month.png", OnGraphGlobalUrlRewriteMonth)
- /graph/urlrewrite_year.png", OnGraphGlobalUrlRewriteYear)
- /graph/urlrewrite_dash.png", OnGraphGlobalUrlRewriteDash)



가상호스트 그래프
------------------------------------
- /graph/vhost/mem_day.png", OnGraphVhostMemDay)
- /graph/vhost/mem_week.png", OnGraphVhostMemWeek)
- /graph/vhost/mem_month.png", OnGraphVhostMemMonth)
- /graph/vhost/mem_year.png", OnGraphVhostMemYear)
- /graph/vhost/mem_dash.png", OnGraphVhostMemDash)
- /graph/vhost/wf2d_day.png", OnGraphVhostWaitingFiles2DeleteDay)
- /graph/vhost/wf2d_week.png", OnGraphVhostWaitingFiles2DeleteWeek)
- /graph/vhost/wf2d_month.png", OnGraphVhostWaitingFiles2DeleteMonth)
- /graph/vhost/wf2d_year.png", OnGraphVhostWaitingFiles2DeleteYear)
- /graph/vhost/wf2d_dash.png", OnGraphVhostWaitingFiles2DeleteDash)
- /graph/vhost/client_httpreq_bypass_day.png", OnGraphVhostClientHttpReqBypassDay)
- /graph/vhost/client_httpreq_bypass_week.png", OnGraphVhostClientHttpReqBypassWeek)
- /graph/vhost/client_httpreq_bypass_month.png", OnGraphVhostClientHttpReqBypassMonth)
- /graph/vhost/client_httpreq_bypass_year.png", OnGraphVhostClientHttpReqBypassYear)
- /graph/vhost/client_httpreq_bypass_dash.png", OnGraphVhostClientHttpReqBypassDash)
- /graph/vhost/client_httpreq_denied_day.png", OnGraphVhostClientHttpReqDeniedDay)
- /graph/vhost/client_httpreq_denied_week.png", OnGraphVhostClientHttpReqDeniedWeek)
- /graph/vhost/client_httpreq_denied_month.png", OnGraphVhostClientHttpReqDeniedMonth)
- /graph/vhost/client_httpreq_denied_year.png", OnGraphVhostClientHttpReqDeniedYear)
- /graph/vhost/client_httpreq_denied_dash.png", OnGraphVhostClientHttpReqDeniedDash)
- /graph/vhost/origin_http_session_day.png", OnGraphVhostOriginHttpSessionDay)
- /graph/vhost/origin_http_session_week.png", OnGraphVhostOriginHttpSessionWeek)
- /graph/vhost/origin_http_session_month.png", OnGraphVhostOriginHttpSessionMonth)
- /graph/vhost/origin_http_session_year.png", OnGraphVhostOriginHttpSessionYear)
- /graph/vhost/origin_http_session_dash.png", OnGraphVhostOriginHttpSessionDash)
- /graph/vhost/origin_traffic_day.png", OnGraphVhostOriginTrafficDay)
- /graph/vhost/origin_traffic_week.png", OnGraphVhostOriginTrafficWeek)
- /graph/vhost/origin_traffic_month.png", OnGraphVhostOriginTrafficMonth)
- /graph/vhost/origin_traffic_year.png", OnGraphVhostOriginTrafficYear)
- /graph/vhost/origin_traffic_dash.png", OnGraphVhostOriginTrafficDash)
- /graph/vhost/origin_http_res_day.png", OnGraphVhostOriginHttpResDay)
- /graph/vhost/origin_http_res_week.png", OnGraphVhostOriginHttpResWeek)
- /graph/vhost/origin_http_res_month.png", OnGraphVhostOriginHttpResMonth)
- /graph/vhost/origin_http_res_year.png", OnGraphVhostOriginHttpResYear)
- /graph/vhost/origin_http_res_dash.png", OnGraphVhostOriginHttpResDash)
- /graph/vhost/origin_http_res_complete_day.png", OnGraphVhostOriginHttpResCompleteDay)
- /graph/vhost/origin_http_res_complete_week.png", OnGraphVhostOriginHttpResCompleteWeek)
- /graph/vhost/origin_http_res_complete_month.png", OnGraphVhostOriginHttpResCompleteMonth)
- /graph/vhost/origin_http_res_complete_year.png", OnGraphVhostOriginHttpResCompleteYear)
- /graph/vhost/origin_http_res_complete_dash.png", OnGraphVhostOriginHttpResCompleteDash)
- /graph/vhost/origin_http_res_detail_day.png", OnGraphVhostOriginHttpResDetailDay)
- /graph/vhost/origin_http_res_detail_week.png", OnGraphVhostOriginHttpResDetailWeek)
- /graph/vhost/origin_http_res_detail_month.png", OnGraphVhostOriginHttpResDetailMonth)
- /graph/vhost/origin_http_res_detail_year.png", OnGraphVhostOriginHttpResDetailYear)
- /graph/vhost/origin_http_res_detail_dash.png", OnGraphVhostOriginHttpResDetailDash)
- /graph/vhost/origin_http_res_time1_day.png", OnGraphVhostOriginHttpTimeDay)
- /graph/vhost/origin_http_res_time1_week.png", OnGraphVhostOriginHttpTimeWeek)
- /graph/vhost/origin_http_res_time1_month.png", OnGraphVhostOriginHttpTimeMonth)
- /graph/vhost/origin_http_res_time1_year.png", OnGraphVhostOriginHttpTimeYear)
- /graph/vhost/origin_http_res_time1_dash.png", OnGraphVhostOriginHttpTimeDash)
- /graph/vhost/origin_http_res_time2_day.png", OnGraphVhostOriginHttpTimeCompleteDay)
- /graph/vhost/origin_http_res_time2_week.png", OnGraphVhostOriginHttpTimeCompleteWeek)
- /graph/vhost/origin_http_res_time2_month.png", OnGraphVhostOriginHttpTimeCompleteMonth)
- /graph/vhost/origin_http_res_time2_year.png", OnGraphVhostOriginHttpTimeCompleteYear)
- /graph/vhost/origin_http_res_time2_dash.png", OnGraphVhostOriginHttpTimeCompleteDash)
- /graph/vhost/client_http_session_day.png", OnGraphVhostClientHttpSessionDay)
- /graph/vhost/client_http_session_week.png", OnGraphVhostClientHttpSessionWeek)
- /graph/vhost/client_http_session_month.png", OnGraphVhostClientHttpSessionMonth)
- /graph/vhost/client_http_session_year.png", OnGraphVhostClientHttpSessionYear)
- /graph/vhost/client_http_session_dash.png", OnGraphVhostClientHttpSessionDash)
- /graph/vhost/client_traffic_day.png", OnGraphVhostClientTrafficDay)
- /graph/vhost/client_traffic_week.png", OnGraphVhostClientTrafficWeek)
- /graph/vhost/client_traffic_month.png", OnGraphVhostClientTrafficMonth)
- /graph/vhost/client_traffic_year.png", OnGraphVhostClientTrafficYear)
- /graph/vhost/client_traffic_dash.png", OnGraphVhostClientTrafficDash)
- /graph/vhost/client_http_res_day.png", OnGraphVhostClientHttpResDay)
- /graph/vhost/client_http_res_week.png", OnGraphVhostClientHttpResWeek)
- /graph/vhost/client_http_res_month.png", OnGraphVhostClientHttpResMonth)
- /graph/vhost/client_http_res_year.png", OnGraphVhostClientHttpResYear)
- /graph/vhost/client_http_res_dash.png", OnGraphVhostClientHttpResDash)
- /graph/vhost/client_http_res_complete_day.png", OnGraphVhostClientHttpResCompleteDay)
- /graph/vhost/client_http_res_complete_week.png", OnGraphVhostClientHttpResCompleteWeek)
- /graph/vhost/client_http_res_complete_month.png", OnGraphVhostClientHttpResCompleteMonth)
- /graph/vhost/client_http_res_complete_year.png", OnGraphVhostClientHttpResCompleteYear)
- /graph/vhost/client_http_res_complete_dash.png", OnGraphVhostClientHttpResCompleteDash)
- /graph/vhost/client_http_res_detail_day.png", OnGraphVhostClientHttpResDetailDay)
- /graph/vhost/client_http_res_detail_week.png", OnGraphVhostClientHttpResDetailWeek)
- /graph/vhost/client_http_res_detail_month.png", OnGraphVhostClientHttpResDetailMonth)
- /graph/vhost/client_http_res_detail_year.png", OnGraphVhostClientHttpResDetailYear)
- /graph/vhost/client_http_res_detail_dash.png", OnGraphVhostClientHttpResDetailDash)
- /graph/vhost/client_http_res_time1_day.png", OnGraphVhostClientHttpTimeDay)
- /graph/vhost/client_http_res_time1_week.png", OnGraphVhostClientHttpTimeWeek)
- /graph/vhost/client_http_res_time1_month.png", OnGraphVhostClientHttpTimeMonth)
- /graph/vhost/client_http_res_time1_year.png", OnGraphVhostClientHttpTimeYear)
- /graph/vhost/client_http_res_time1_dash.png", OnGraphVhostClientHttpTimeDash)
- /graph/vhost/client_http_res_time2_day.png", OnGraphVhostClientHttpTimeCompleteDay)
- /graph/vhost/client_http_res_time2_week.png", OnGraphVhostClientHttpTimeCompleteWeek)
- /graph/vhost/client_http_res_time2_month.png", OnGraphVhostClientHttpTimeCompleteMonth)
- /graph/vhost/client_http_res_time2_year.png", OnGraphVhostClientHttpTimeCompleteYear)
- /graph/vhost/client_http_res_time2_dash.png", OnGraphVhostClientHttpTimeCompleteDash)
- /graph/vhost/client_http_res_hit_day.png", OnGraphVhostClientHttpResHitDay)
- /graph/vhost/client_http_res_hit_week.png", OnGraphVhostClientHttpResHitWeek)
- /graph/vhost/client_http_res_hit_month.png", OnGraphVhostClientHttpResHitMonth)
- /graph/vhost/client_http_res_hit_year.png", OnGraphVhostClientHttpResHitYear)
- /graph/vhost/client_http_res_hit_dash.png", OnGraphVhostClientHttpResHitDash)
- /graph/vhost/client_traffic_ssl_day.png", OnGraphVhostClientTrafficSSLDay)
- /graph/vhost/client_traffic_ssl_week.png", OnGraphVhostClientTrafficSSLWeek)
- /graph/vhost/client_traffic_ssl_month.png", OnGraphVhostClientTrafficSSLMonth)
- /graph/vhost/client_traffic_ssl_year.png", OnGraphVhostClientTrafficSSLYear)
- /graph/vhost/client_traffic_ssl_dash.png", OnGraphVhostClientTrafficSSLDash)
- /graph/vhost/hitratio_day.png", OnGraphVhostHitRatioDay)
- /graph/vhost/hitratio_week.png", OnGraphVhostHitRatioWeek)
- /graph/vhost/hitratio_month.png", OnGraphVhostHitRatioMonth)
- /graph/vhost/hitratio_year.png", OnGraphVhostHitRatioYear)
- /graph/vhost/hitratio_dash.png", OnGraphVhostHitRatioDash)
- /graph/vhost/filecount_day.png", OnGraphVhostFileCountDay)
- /graph/vhost/filecount_week.png", OnGraphVhostFileCountWeek)
- /graph/vhost/filecount_month.png", OnGraphVhostFileCountMonth)
- /graph/vhost/filecount_year.png", OnGraphVhostFileCountYear)
- /graph/vhost/filecount_dash.png", OnGraphVhostFileCountDash)
