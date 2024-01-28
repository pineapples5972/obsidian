---
{"dg-publish":true,"permalink":"/dev-ops/terraform/terraform-commands/"}
---

#terraform #commands 

![Pasted image 20240117094903.png](/img/user/metadata/attachments/Images/Pasted%20image%2020240117094903.png)
### Init
after writing the terraform file we can run `terraform init` command

Init command will check the configuration file and initialize the working directory cotntaining .tf file.
![Pasted image 20240117094314.png](/img/user/metadata/attachments/Images/Pasted%20image%2020240117094314.png)

### Plan
Next run `terraform plan`
To review the execucation plan that will be carried out by terraform.
It will displayed the list of actions that will be taken by terraform.
and the changes that going to happen.
This will also shows the changes we did not specified. These are the values that are neccessary to make resources work fine terraform take care of this for you.

![Pasted image 20240117094539.png](/img/user/metadata/attachments/Images/Pasted%20image%2020240117094539.png)
### Apply
`terraform apply`  
After the review we can create the resources with this command.
This command will display the execution plan once again to ensure everything is going according to plan and ask for user's confirmation and apply the changes.

![Pasted image 20240117095046.png](/img/user/metadata/attachments/Images/Pasted%20image%2020240117095046.png)

### Show
`terraform show`
while we can always check manually if our files and resources created,
running `terraform show` in the configuration file directory it will show the details of the resources that you are just created. This command inspect the state file and displays the resource details.
![Pasted image 20240117100333.png](/img/user/metadata/attachments/Images/Pasted%20image%2020240117100333.png)
Additionally you can display the same information with json format with `terraform show -json`.

### Destroy
`terraform destroy`

To destroy the resources and clean the infrastructure we can use this command.
### Validate
`terraform validate`

### Format
`terraform fmt`

### Providers
`terraform providers`
`terraform providers mirror /root/terraform/new_local_file`


### Output 
`terraform output`

### Refresh - if there is any manual update, it refreshes the state file
`terraform refresh`

	### Graph
`terraform graph`
apt install graphviz
`terraform graph | dot -Tsvg > graph.svg`

	![[Pasted image 20231208201331.png\|Pasted image 20231208201331.png]]
	




The `terraform apply` failed in spite of our validation working! This is because the validate command only carries out a general verification of the configuration. It validated the resource block and the argument syntax but not the `values` the arguments expect for a specific resource!



### State list
`terraform state list`
