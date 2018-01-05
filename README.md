<?php
	
	//Declaring global variables
	$username;
	$firstname;
	$lastname;
	$email;
	$accountNumber;
	$balance;
	$user;
	$accountType;
	$bankName;
	$ifscCode;
	
	//Setting variable types
	settype($username, "string");
	settype($firstname, "string");
	settype($lastname, "string");
	settype($emailname, "string");
	settype($accountNumber, "int");
	settype($balance, "double");
	
	interface parameterisedMethods{
		function Deposit($amount);
		function Withdraw($amount);
		function transferOwnBank($userAccountNumber, $amount);
		function transferDifferentBank($userAccountNumber, $ifsc, $amount);
	}
	
	abstract class nonParameterisedMethods{
		abstract function getName();
		abstract function getBalance();
		public function getAccountNumber(){
			
		}
	}
	
	class BankAccount extends nonParameterisedMethods implements parameterisedMethods{
		
		public function getName(){
			
			return $this->user; 
		}

		public function getBalance(){
			
			if(($this->balance) > 0){
				return $this -> balance;

			} else if(($this->balance) <= 0 ){
				return 'Balance is empty '; 
				
			}else{
				return 'error'; 
			}   
		}
			
		 public function getAccountNumber(){
			 
			return $this->accountNumber; 
		}
		
		public function Deposit($amount){
			
			if($amount > 49000){
				echo "Deposit cant be greater than 49000</br>";
				
			}else{
				$this->balance = $this->balance + $amount;  
				echo "You have Deposited: ".$amount."</br>";
				echo "After Deposit Balance is: ".$this->balance."</br>";
				
			}
		}


		public function Withdraw($amount){

			if($this->accountType == "Deposit"){
				$this->balance = $this->balance - $amount; 
				echo "You have Withdrawed: ".$amount."</br>";
				echo "After Withdraw Balance is: ".$this->balance."</br></br>";
				
			}elseif($amount > 10000){
				echo "Withdrawal cant be greater than 10000.</br></br>";

			}elseif(($this->balance) < $amount){
				echo "Not enough funds to withdraw.</br></br>";

			}else{
				$this->balance = $this->balance - $amount; 
				echo "You have Withdrawed: ".$amount."</br>";
				echo "After Withdraw Balance is: ".$this->balance."</br></br>";
			}
		}  
		
		public function transferOwnBank($userAccountNumber, $amount){
	
			echo "<h3><strong>A ".$this->bankName." to ".$userAccountNumber->bankName." Transfer.</strong></h3></br>";
	
			if(($this->balance) < $amount){
				echo "Not enough funds.</br>";
				
			}elseif($userAccountNumber->accountNumber != 1346){
				echo "Invalid Account Number.</br>";

			}else{
				$this->balance = $this->balance - $amount; 
				$userAccountNumber->balance = $userAccountNumber->balance + $amount;
				echo "Transferred: ".$amount." from: ".$this->user." to: ".$userAccountNumber->user."</br>";
				echo "After Transfer, Balance of ".$this->user." is: ".$this->balance."</br></br>";
			}
		}  
		
		public function transferDifferentBank($userAccountNumber, $ifsc, $amount){
			
			echo "<h3><strong>A ".$this->bankName." to ".$userAccountNumber->bankName." Transfer.</strong></h3></br>";
			
			if(($this->balance) < $amount){
				echo "Not enough funds.</br>";
				
			}elseif($userAccountNumber->accountNumber != 1278){
				echo "Invalid Account Number";
				
			}elseif($ifsc->ifscCode != "SBIN10078"){
				echo "Invalid IFSC";
				
			}else{
				$this->balance = $this->balance - $amount; 
				$userAccountNumber->balance = $userAccountNumber->balance + $amount;
				echo "Transferred: ".$amount." from: ".$this->user." to: ".$userAccountNumber->user."</br>";
				echo "After Transfer, Balance of ".$this->user." is: ".$this->balance."</br></br>";
			}
		}  
	}
	
	//Instance for user1
	$user1 = new BankAccount();
	
	//Setting Properties
	$user1->username="yash@123";
	$user1->firstname="Yash ";
	$user1->lastname="Patel";
	$user1->email="yash@123.com";
	$user1->accountNumber=1234;
	$user1->balance=1000;
	$user1->accountType="Saving";
	$user1->bankName="SBI";
	$user1->ifscCode="SBIN10078";
	$user1->user= $user1->firstname.$user1->lastname;
	
	//Printing Properties
	echo "<h3><strong>A SBI Bank Cusutomer</strong></h3></br>";
	echo "Customer Name is: ".$user1->user."</br>";
	echo "Customer Username is: ".$user1->username."</br>";
	echo "Customer Email is: ".$user1->email."</br>";	
	echo "Customer Account Number is: ".$user1->accountNumber."</br>";
	echo "Customer Bank Name is: ".$user1->bankName."</br>";
	echo "Customer Account Type is: ".$user1->accountType."</br>";
	echo "Initial Balance is: ".$user1->balance."</br>";
		
	//Deposit
	$user1->Deposit(30000);
	
	//Withdraw
	$user1->Withdraw(2000);
	
	
	
	//Instance for user2
	$user2 = new BankAccount();
	
	//Setting Properties
	$user2->username="harsh@978";
	$user2->firstname="Harsh ";
	$user2->lastname="Patel";
	$user2->email="hp0494@mail.com";
	$user2->accountNumber=1278;
	$user2->balance=2000;
	$user2->accountType="Saving";
	$user2->bankName="SBBJ";
	$user2->user= $user2->firstname.$user2->lastname;
	
	//Printing Properties
	echo "<h3><strong>A SBBJ Bank Cusutomer</strong></h3></br>";	
	echo "Customer Name is: ".$user2->user."</br>";
	echo "Customer Username is: ".$user2->username."</br>";
	echo "Customer Email is: ".$user2->email."</br>";	
	echo "Customer Account Number is: ".$user2->accountNumber."</br>";
	echo "Customer Bank Name is: ".$user2->bankName."</br>";
	echo "Customer Account Type is: ".$user2->accountType."</br>";
	echo "Initial Balance is: ".$user2->balance."</br>";
		
	//Deposit
	$user2->Deposit(3000);
	
	//Withdraw
	$user2->Withdraw(1000);
	
	
	
	//Instance for user3
	$user3 = new BankAccount();
	
	//Setting Properties
	$user3->username="tejas@1997";
	$user3->firstname="Tejas ";
	$user3->lastname="Patel";
	$user3->email="tejas97@mail.com";
	$user3->accountNumber=1346;
	$user3->balance=3100;
	$user3->accountType="Deposit";
	$user3->bankName="SBI";
	$user3->user= $user3->firstname.$user3->lastname;
	
	//Printing Properties
	echo "<h3><strong>A SBI Bank Cusutomer</strong></h3></br>";	
	echo "Customer Name is: ".$user3->user."</br>";
	echo "Customer Username is: ".$user3->username."</br>";
	echo "Customer Email is: ".$user3->email."</br>";	
	echo "Customer Account Number is: ".$user3->accountNumber."</br>";
	echo "Customer Bank Name is: ".$user3->bankName."</br>";
	echo "Customer Account Type is: ".$user3->accountType."</br>";
	echo "Initial Balance is: ".$user3->balance."</br>";
		
	//Deposit
	$user3->Deposit(10000);
	
	//Withdraw
	$user3->Withdraw(200);
	
	//Transfer in Same Bank
	$user1->transferOwnBank($user3, 1000);

	//Transfer in Different Bank
	$user1->transferDifferentBank($user2, $user1, 5000);
	
	
