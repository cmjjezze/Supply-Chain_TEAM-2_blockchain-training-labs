#  Hyperledger Training
## Use Case: Invoice

### Device Information
```bash
Operating System : Linux Ubuntu 18.04 LTS || 64-bit
CPU : Intel® Core™ i5-7200U CPU @ 2.50GHz × 4 
Memory : 11.6 GiB
Graphics : GeForce 940MX/PCIe/SSE2 
Disk : 245.1 GB
```


### Install all the of required development. It is found in the 
```bash
https://hyperledger.github.io/composer/latest/installing/installing-prereqs.html.
```

Add installation in golang:
1. Go to https://golang.org/dl/ for the compatibility of the device using.
2. After downloading the tar file, extract it in the terminal and paste this command:
   ```bash
   sudo tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
   ```
3. Next, add a directory path environment in .profile. Open the terminal and type nano ~/.profile, then paste this command and save: <br>
   ```bash
   export PATH=$PATH:/usr/local/go/bin;
   ```
4. Lastly, type this command to refresh the .profile file: source ~/.profile.
Also install a postman for the testing part. If you are using the ubuntu, just downloaded it in the ubuntu software.


### Download or clone this repository.
Step 1. Open the terminal and type: nvm use 8. This command is for the compatibility of node in hyperledger. <br>
Step 2. Go to the folder that you clone earlier and go to the directory of invoice.
```bash
cd fabric-samples/invoice
```
Step 3. Start the fabric server. <br>
```bash
> hyperledger@ubuntu:~/fabric-samples/invoice$./startFabric.sh
```
//This procedure is the starting of the chaincode.
//If there is an error, just type this command: <br>
```bash
> $docker kill $(docker ps -q)
> $docker rm $(docker ps -aq)
> $docker rmi $(docker images dev-* -q)
```
//This command is for stopping and deleting the docker images and container that containing the fabric chaincode <br>

Step 4. Next, type this command in the terminal:
```bash
> node enrollAdmin.js
```
//This is the enrolling of admin in the hyperledger. It will give a certificate that is needed.<br>

Step 5. Next, add a user.
```bash
> node registerUser.js
```


## Guide of users:
IBM - Supplier <br>
Lotus - OEM <br>
UBP - Bank <br>
<br>
//This is the adding or register the three user. The supplier, bank and the OEM or the Object Efficiency Management.
```bash
> node app.js
```
Step 7. Open the postman and put the method in Get and type the localhost:3000. Click the body. Add a username and Supplier or any user that we register earlier in the key and value respectively. <br>
//Supplier, Bank or OEM are the registered user.
//This will give the initiate record in the function initLedger in the invoice.go file. It is located in the invoice folder by the chaincode folder.

Step 8. Adding a invoice. <br>
> Change the GET method into POST and type the 

```bash
localhost:3000/invoice
```
> Click the body and add the these key and values:

```bash
key         value
username        Lotus
invoiceId       INV1 //stands for invoice1
invoiceNumber       001
billedTo        Bank
invoiceDate     02/12/19
invoiceAmount       5000
itemDescription     Case //Description of the item
gr          No //GR is Good Received
isPaid          No
paidAmount      0
repaid          No
repaymentAmount     0
```
<br>

> Click send
<br>

//If you put Bank or OEM in the username value, it will have a error because only the supplier can add a invoice.
For viewing the new invoice: just do the step 7. <br>
Step 9. Bank paying the Supplier <br>
> Change the POST method into PUT and dont change the localhost:3000/invoice. <br>
> In postman there is a checkbox for disabling the key values. Disable all the key except the invoiceId, username and paidAmount. <br>
> Change the username value of UBP, invoiceId is INV1 and put a any value in the paidAmount. Paid Amount value should be lowered in the invoiceAmount. Since we put the invoiceAmount in 5000, you should input a value for paidAmount less than 5000. <br>
> Click Send
<br>
//There is also an error if you put Supplier or OEM in the username value. Only the bank should pay the supplier.
For viewing the new invoice: just do the step 7.<br>

Step 10. OEM paying the Bank <br>
> Don't change anything in the method and localhost. <br>
> In postman there is a checkbox for disabling the key values. Disable all the key except the invoiceId, username and repayAmount. Make sure that the paidAmount is disable. <br>
> Change the username value of OEM, invoiceId is INV1 and put a any value in the repaymentAmount. Repayment Amount value should be greater than the paidAmount. <br>
> Click Send
<br>
//There is also an error if you put Supplier or Bank in the username value. Only the bank should pay the supplier.
For viewing the new invoice: just do the step 7. <br>

Step 11. Goods Received. <br>
> Don't change anything in the method and localhost.
> Disabled the fields except for the username, invoiceId and gr.
> Change the values into Supplier, INV1, Y respectively.
> Click Send
//There is also an error if you put Supplier or Bank in the username value. Only the bank should pay the supplier.
For viewing the new invoice: just do the step 7. <br>

Step 12. Transaction Log <br>
> Change the method into GET and localhost:3000
> Disable all the key except the username and invoiceId.
> Put the respectively value: UBP and INV1.
//Any username may do.
> Click send.
//You will see the transaction that we did.
//Any username will do.
