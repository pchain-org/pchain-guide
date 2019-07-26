.. _AWS:

============================
Install From AWS Marketplace
============================

Pchain is listing on AWS Marketplace, you can subscribe from `AWS Marketplace <https://aws.amazon.com/marketplace/pp/B07VNFPPXZ>`_. Please follow the step:

Click Continue to Subscribe:

.. image:: ../_static/aws/0.png

Click Accept Terms:

.. image:: ../_static/aws/1.png

Click Continue to Configuration:

.. image:: ../_static/aws/2.png

We recommend US West(Oregon) region, and clean Continue to Launch:

.. image:: ../_static/aws/3.png

We recommend t3.large:

.. image:: ../_static/aws/4.png

And click Create New Based On Seller Settings:

.. image:: ../_static/aws/5.png

.. image:: ../_static/aws/6.png

After launch, you can go to EC2 console:

.. image:: ../_static/aws/7.png

And edit the security group:

.. image:: ../_static/aws/9.png

.. image:: ../_static/aws/8.png

Open port 6969 and 22 to your local ip:

.. image:: ../_static/aws/10.png

Attach to your aws ec2, run command
::	
	cd pchain
	./run.sh
	./bin/pchain attach .pchain/pchain/pchain.ipc

and check eth.blockNumber to see if the height changes continiously.

.. image:: ../_static/aws/11.png

After that, exit console and set up the crontab by command "sudo crontab -u ubuntu scripts/pchain.cron", and run "crontab -l" to check.

.. image:: ../_static/aws/12.png

Now you can go :ref:`Create Your Account`.
