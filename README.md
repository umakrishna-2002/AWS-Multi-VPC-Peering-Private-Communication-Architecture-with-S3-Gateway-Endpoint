 AWS Multi VPC Peering Private Communication Architecture with S3 Gateway Endpoint
The follwoing project implements secure connection between tow VPC's using VPC peering.
Workflow goes as follows:
1. Creating twi VPC's in us-west-1 (Oregon) region.
2. Connecting through VPC Peering.
3. Accessing the S3 through one of the private instance using S3 Gateway wothout using the internet.
![image](https://github.com/user-attachments/assets/5f0dd5f8-d3db-490e-a7ad-545d75b760ef)

Create two VPC's in Oregon region
VPC should consists of:
- Two subnets one is public and the other private.
- Create Internet Gateway and attach it to the Public Routable so that Public Route Table along with associating the Public subnet to it.
![image](https://github.com/user-attachments/assets/5e7fe322-1c42-4085-b4f1-633e0c91ccd7)

Similarly for the second VPC:
- Two subnets one is public and the other private.
- Create Internet Gateway and attach it to the Public Routable so that Public Route Table along with associating the Public subnet to it.
  ![image](https://github.com/user-attachments/assets/8c4dbc68-2e97-4f56-bd76-98dcd4a9af0a)

Now create a Peering Connection between two VPC's
![image](https://github.com/user-attachments/assets/6521b53f-c776-4411-87bf-47f2242c39a3)

Now add the Private subnet id of the first vpc in the Private Route table of the second VPC.
![image](https://github.com/user-attachments/assets/969cdfde-0848-4d34-8f2c-5c515d63b06c)

Similarly, add Private subnet id of the second vpc in the Private Route table of the first VPC and establish peering connection between two VPC's
![image](https://github.com/user-attachments/assets/3e8b7592-9b86-41a3-b63e-385ba7596419)

Create EC2 instance by adding the VPC and subnets respectively. 
Instances created using first VPC and their public and private subnets.
![image](https://github.com/user-attachments/assets/55333392-35b3-43bb-aff6-117f275f5670)

Instances created using second VPC and their public and private subnets.
![image](https://github.com/user-attachments/assets/af516b32-871c-4161-8258-176949945319)

Check the peering connection by ssh into the private instances through the public instance.
APP-Public instance which is associated with Public Subnet.
![image](https://github.com/user-attachments/assets/2a283e8d-9b4b-4e6a-93f3-477904de7490)

App-Private instances is connected through App-Public instance.
![image](https://github.com/user-attachments/assets/f4c6802d-560f-4d6f-9e48-122c9f6a9e37)

Similarly for Data- Private instance is connected through Data-Public Instance.
![image](https://github.com/user-attachments/assets/4eb6c32d-7dca-4da1-92c1-74632d3de7e6)

Now we can check the peering connection between private instance with the help of their private Ip's
![image](https://github.com/user-attachments/assets/d86290c9-6561-4f3b-bd83-53b6af4e155d)

![image](https://github.com/user-attachments/assets/2112b094-d514-4383-a1f2-e7152dc206fc)

Create S3 Gateway VPC Endpoint
Give a name and choose AWS services.
![image](https://github.com/user-attachments/assets/e7afb030-0864-436d-aa7f-e8d921941fe7)

Under AWS srvices 
-choose s3 and choose Gateway
![image](https://github.com/user-attachments/assets/bae5130a-d076-4747-b72c-136abd6d1260)

For Network settings
- Choose the desired VPC i.e., Data VPC through we want to access the S3.

- ![image](https://github.com/user-attachments/assets/020ed368-b448-401c-a7c4-84a573a243dd)
- Choose the Route Table for which the Private subnet is associated.
![image](https://github.com/user-attachments/assets/90966898-d2c0-4fee-8302-7692b864052e)

S3 Gateway is created and assocaited with Private instance.
![image](https://github.com/user-attachments/assets/1752a579-b2f5-487e-b401-d46beb2af70a)

We can see that the created S3 Gateway is attached to the Data Private RT.
![image](https://github.com/user-attachments/assets/e09f2fcf-7ffe-4aeb-988d-2bf1e53359e7)

Now access the S3 through the Data Private instance.
![image](https://github.com/user-attachments/assets/01984304-3a6a-44d6-8354-ddbba2830556)

