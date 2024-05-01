# ps-visio
Atividade desenvolvida para o processo seletivo da vaga de estágio da Visio

Como acessar a aplicação:

    1.Clonar/baixar o repositório
    
    2.Entrar na pasta: cd ps-visio-main/

    3.Alterar a linha 16 do arquivo prometheus.yml (para o node exporter funcionar) => SEU_IP:9100

    4.Executar: docker compose up -d

    5.Executar os seguintes contêineres para restaurar os dados do Prometheus e do Grafana

	    5.1. docker run --user root --rm --mount source=ps-visio-main_grafana_data,target=/var/lib/grafana -v $(pwd):/backup busybox /bin/sh -c "chown 472:0 /var/lib/grafana && chmod 777 /backup/grafana.db && cp /backup/grafana.db /var/lib/grafana/grafana.db && chmod 777 /var/lib/grafana/grafana.db"
	    
	    5.2. docker run --user root --rm --mount source=ps-visio-main_prometheus_data,target=/prometheus -v $(pwd):/backup busybox cp -rf /backup/prometheus-data /prometheus

    6.Restart o compose para aplicar as mudanças
    
    	docker compose restart

    7.Acessar os serviços em

        7.1.Grafana: http://localhost:4000
            
            - Login: admin
            - Senha: 123123

        7.2.Prometheus: http://localhost:9090

    8.Para parar as aplicações, executar: "docker compose down"
