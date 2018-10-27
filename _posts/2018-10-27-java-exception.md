---
title: "Java Exception Notes"
layout: post
date: 2018-10-25
# image: /assets/images/adsk.JPG
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

## Exception Hierarchy
Throwable 
* Exception
    * ClassNotFoundException
    * IOException
        * FileNotFoundException
    * RunTimeException
        * NullPointerException
        * ArrayIndexOutOfBoundsException
* Error - beyond control of progrmamer
    * VirtualMachineError
        * OutOfMemoryError

## Example of try-with-resources
```
import java.io.File;
import java.io.FileReader;
import java.io.IOException;

public class ReadData {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("file path")) {
            System.out.println(fr.nextLine());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fr.close();
            } catch (IOException ex) {
                ex.printStackTrace();
            }
        }
    }
}
```

## Example
* throws exception for upper level to handle

```
import java.io.*;

public class InsufficientFundsException extends Exception {
    private double amount;
    
    public InsufficientFundsException(double amount) {
        this.amount = amount;
    }
    
    public double getAmount() {
        return this.amount;
    }
}

public class CheckingAccount {
    private double balance;
    private int id;

    public CheckingAccount(int x) {
        this.id = x;
    }

    public void deposit (double amount) {
        this.balance += amount;
    }

    public void withdraw(double amount) throws InsufficientFundsException {
        if (this.balance >= amount) {
            balance -= amount;
        } else {
            double need = amount - balance;
            throw new InsufficientFundsException(need);
        }
    }

    public double getBalance() {
        return this.balance;
    }

    public int getId() {
        return this.id;
    }
}

public class BankDemo {
    public static void main(String[] args) {
        CheckingAccount myAccount = new CheckingAccount(1);
        myAccount.deposit(200.0);

        try {
            myAccount.withdraw(100.0);
            myAccount.withdraw(300.0);
        } catch (InsufficientFundsException e) {
            e.printStackTrace();
        }
    }
}

```