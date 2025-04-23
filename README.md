# mongodb-statefulset

## Prerequisites 

* EKS cluster setup with kubectl
* eksctl and aws should be configured
* kubectl access to eks cluster
* Install the EBS CSI driver

    you can do this by running the following commands :

      eksctl create iamserviceaccount \
		  --name ebs-csi-controller-sa \
		  --namespace kube-system \
		  --cluster <your-cluster-name> \
		  --attach-policy-arn arn:aws:iam::aws:policy/service-role/AmazonEBSCSIDriverPolicy \
		  --approve \
		  --role-name AmazonEKS_EBS_CSI_DriverRole
		
		eksctl utils associate-iam-oidc-provider \
		  --region <region> \
		  --cluster <your-cluster-name> \
		  --approve
		
		eksctl create addon --name aws-ebs-csi-driver \
		  --cluster <your-cluster-name> \
		  --service-account-role-arn arn:aws:iam::<account-id>:role/AmazonEKS_EBS_CSI_DriverRole \
		  --force


