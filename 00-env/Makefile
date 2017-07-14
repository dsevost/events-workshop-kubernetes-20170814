.PHONY: vms hosts kube clean

#up: vms host kube

clean: kube-clean

kube-clean:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 kubernetes.yaml --tags clean

vms:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 vms.yaml --tags create

vms-test:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 vms-test.yaml --tags test -v

vms-start:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 vms.yaml --tags start

host:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 host.yaml

#docker:
#	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 docker.yaml

kube:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 kubernetes.yaml --tags create
flannel:
	ansible-playbook -i inventory/events-workshop-kubernetes-20170814 flannel.yaml --tags create
