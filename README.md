# ps-visio
Atividade desenvolvida para o processo seletivo da vaga de estágio da Visio

Como acessar a aplicação:

    1.Clonar o repositório

    2.Executar: docker compose up -d

    3.Executar os seguintes contêineres para restaurar os dados do Prometheus e do Grafana

	    3.1. docker run --user root --rm --mount source=ps-visio-main_grafana_data,target=/var/lib/grafana -v $(pwd):backup busybox /bin/sh -c "chown 472:0 /var/lib/grafana && chmod 777 /backup/grafana.db && cp /backup/grafana.db /var/lib/grafana/grafana.db && chmod 777 /var/lib/grafana/grafana.db"
	    
	    3.2. docker run --user root --rm --mount source=ps-visio-main_prometheus_data target=/prometheus -v $(pwd):backup busybox tar -xzvf /backup/prometheus-data.tar.gz -C
    
    4.Restart o compose para aplicar as mudanças
    
    	docker compose restart

    5.Acessar os serviços em

        5.1.Grafana: http://localhost:4000
            
            - Login: admin
            - Senha: 123123

        5.2.Prometheus: http://localhost:9090

    6.Para parar as aplicações, executar: "docker compose down"
