#.PHONY: vms hosts kube clean

#up: vms host kube

all:				# The Help
	@echo Public targets
	@ grep '^[a-z-]\+:\s\+#' Makefile

clean: kube-clean

kube-clean:
	ansible-playbook kubernetes.yaml --tags clean

vms: 				# Provision VMs
	ansible-playbook vms.yaml --tags create

#vms-test:
#	ansible-playbook vms-test.yaml --tags test -v

#vms-start:
#	ansible-playbook vms.yaml --tags start

host:				# Setup Hosts
	ansible-playbook host.yaml

docker:
	ansible-role .docker.yaml

kube:				# Install Kubernetes Cluster
	ansible-playbook kubernetes.yaml --tags create

flannel:
	ansible-playbook .flannel.yaml --tags create

get-all:			# Show artifacts artifacts
	ansible master-client -m command -a 'kubectl get all -o wide'

create-helloworld:		# Create hello-world deployment
	ansible master-client -m command -a 'kubectl run hello-world --image=tutum/hello-world  --port=80'

expose-helloworld:		# Expose hello-world service
	ansible master-client -m command -a 'kubectl expose deploy hello-world --port=80 --target-port=80 --name hello-svc'


test-helloworld:		# Test hello-world container
	ip=$$(ansible master-client -m command -a 'kubectl get svc hello-svc -o jsonpath="SVC:{ .spec.clusterIP }"' 2>&1 | \
	  awk -F: '/SVC/ { print $$2; }') ; \
	  echo $$ip ; \
	ansible master-client -m command -a "curl $$ip"


scale-helloworld:		# Scale hello-world container
	ansible master-client -m command -a 'kubectl scale deploy hello-world --replicas=3'

kill-helloworld:		# Kill running container instance
	ansible master-client -m command -a 'kubectl delete pod -l run=hello-world'

remove-helloworld:		# Remove hello-world artifacts
	ansible master-client -m command -a 'kubectl delete all -l run=hello-world'

#build-eap-ds-test:		# Create Docker Image for JBoss EAP Web Application
#	sudo docker pull jboss-eap-7/eap70-openshift
#	h=$$HOME ; \
#	sudo $$h/bin/s2i build https://github.com/dsevost/eap-6-pg-test jboss-eap-7/eap70-openshift eap-ds-test
