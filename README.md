# CVE-2021-22005

VMware vCenter RCE CVE-2021-22005 one-liner mass checker

cat vmware_centers.txt | while read S do; do curl --connect-timeout 15 --max-time 30 --silent --insecure --user-agent "vAPI/2.100.0 Java/1.8.0_261 (Linux; 4.19.160-6.ph3; amd64)" -X POST "https://$S/analytics/telemetry/ph/api/hyper/send?_c&_i=test" -d "lorem ipsum" -H "Content-Type: application/json" -L --stderr - -v | tac | grep -q "HTTP/1.1 201" && printf "$S \033[1;35mVulnerable\e[0m\n" || printf "$S \033[1;32mPatched\e[0m\n"; done;
