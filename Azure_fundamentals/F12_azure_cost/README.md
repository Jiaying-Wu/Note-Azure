Predict costs and optimize spending for Azure
================

This notebook is refer from the Microsoft resources: [Azure fundamentals](https://docs.microsoft.com/en-gb/learn/paths/azure-fundamentals/).

Cost is one of the most important aspects of the cloud and can have a massive impact on your business. Azure has several tools available to help you get a better understanding of cloud spend and some best practices that you can leverage to help you save money.

### Topic 1: Introduction

When planning a solution in the cloud, there's always the challenge of **balancing cost against performance**. It can feel like a guessing game whether your selected options will stay within budget or if you'll have a surprise on your next bill.

You need to be able to confidently answer several questions:

-   What will this solution cost this fiscal year?

-   Is there an alternate configuration you could use to save money?

-   Can you estimate how a change would impact your cost and performance without putting it into a production system?

In this module, we'll explore the tools you can use to answer these questions and more.

#### Learning objectives

In this module, you will:

-   Learn the different options you have to purchase Azure services

-   Estimate costs with the Azure pricing calculator

-   Predict and optimize costs with Azure Cost Management and Azure Advisor

-   Apply best practices for saving on infrastructure costs

-   Apply best practices for saving on licensing costs

### Topic 2: Purchase Azure products and services

Products and services in Azure are arranged by category, with various resources that you can provision. You select the Azure products and services that fit your requirements, and your account is billed according to Azure's pay-for-what-you-use model.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/1a-azure-products-overview.png)

#### 2.1 Usage meters

When you provision an Azure resource, Azure creates one or more meter instances for that resource. The meters track the resources' usage, and generate a usage record that is used to calculate your bill.

For example, a single virtual machine that you provision in Azure might have the following meters tracking its usage:

-   Compute Hours

-   IP Address Hours

-   Data Transfer In

-   Data Transfer Out

-   Standard Managed Disk

-   Standard Managed Disk Operations

-   Standard IO-Disk

-   Standard IO-Block Blob Read

-   Standard IO-Block Blob Write

-   Standard IO-Block Blob Delete

The meters and pricing vary per product and often have different pricing tiers based on the size or capacity of the resource. Check the documentation for specific details on what each service area costs.

At the end of each monthly billing cycle, the usage values will be charged to your payment method and the meters are reset. You can check the billing page in the Azure portal at any time to get a quick summary of your current usage and see any invoices from past billing cycles.

The key takeaway is that resources are always charged based on usage. For example, if you de-allocate a VM then you will not be billed for compute hours, I/O reads or writes or the private IP address since the VM is not running and has no allocated compute resources. However you will incur storage costs for the disks.

![](../image/F12_usage_note.png)

### Topic 3: Factors affecting costs

Just like your on-premises equipment costs, there are several elements that will affect your monthly costs when using Azure services. Let's look at a few of the primary factors including resource type, services, the user's location, and the billing zone.

#### 3.1 Resource type

Costs are resource-specific, so the usage that a meter tracks and the number of meters associated with a resource depend on the resource type.

![](../image/F12_resource_note.png)

The usage that a meter tracks correlates to a number of billable units. The rate per billable unit depends on the resource type you are using. Those units are charged to your account for each billing period.

#### 3.2 Services <img src="https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/2b-billing-period-graphic.png" heigth="8%" style="width:8.0%" />

Azure usage rates and billing periods can differ between Enterprise, Web Direct, and Cloud Solution Provider (CSP) customers. Some subscription types also include usage allowances, which affect costs.

The Azure team develops and offers first-party products and services, while products and services from third-party vendors are available in the [Azure Marketplace](https://azuremarketplace.microsoft.com/). Different billing structures apply to each of these categories.

#### 3.3 Location

Azure has datacenters all over the world. Usage costs vary between locations that offer particular Azure products, services, and resources based on popularity, demand, and local infrastructure costs.

For example, you might want to build your Azure solution by provisioning resources in locations that offer the lowest prices. This approach, though, would require transferring data between locations if any dependent resources and their users are located in different parts of the world. If there are meters tracking the volume of data moving between the resources you provision, any potential savings you make from choosing the cheapest location could be offset by the additional cost of transferring data between those resources.

#### 3.4 Azure billing zones <img src="https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/1b-azure-regions-globe.png" heigth="8%" style="width:8.0%" />

**Bandwidth refers to data moving in and out of Azure datacenters**. Most of the time inbound data transfers (data going into Azure datacenters) are free. For outbound data transfers (data going out of Azure datacenters), the data transfer pricing is based on **Billing Zones**.

**A Zone is a geographical grouping of Azure Regions for billing purposes**. The following zones exist and include the listed countries (regions).

![](../image/F12_billing_zone.png)

In most zones, the first outbound 5 gigabytes (GB) per month are free. After that amount, you are billed a fixed price per GB.

![](../image/F12_zone_note.png)

### Topic 4: Exercise - Estimate costs with the Azure pricing calculator

Imagine that you've been asked to build a system on Azure, and you've been asked for an estimate of what it might cost to run over the next 12 months. You already know that Azure pricing is fully transparent and that you're billed monthly for only the services that you use. How would you get that estimate without deploying and running those services or without manually pricing out each service from the Azure service pricing pages?

#### 4.1 Introducing the Azure pricing calculator

To make estimates easy for customers to create, Microsoft developed the Azure pricing calculator. The Azure pricing calculator is a free web-based tool that allows you to input Azure services and modify properties and options of the services. It outputs the costs per service and total cost for the full estimate.

The options that you can configure in the pricing calculator vary between products, but basic configuration options include:

![](../image/F12_caculator_option.png)

##### 4.2.1 Try out the Azure pricing calculator

In another browser window or tab, open the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/). On the pricing calculator page, you'll see several tabs:

1.  **Products**. This tab is where you'll do most of your activity. This tab has all the Azure services listed and is where you'll add or remove services to put together your estimate.

2.  **Example Scenarios** This tab has several examples of infrastructure involved in common cloud-based solutions. You can add all the components of the entire scenario to estimate the cost.

3.  **Saved Estimates**. This tab has all of your previously saved estimates. We'll go through this process in a moment.

4.  **FAQ**. Just as it says, this tab has answers to some frequently asked questions.

Let's start with the **Products** tab. You'll see the full listing of service categories down the left-hand side. Clicking on any of the categories will display the services in that category. There's also a search box where you can search through all services for the service you're looking for. Clicking on the service will add it to your estimate. You can add just one service, or you can add as many as you need, including multiples of the same service. For example, you can add multiple virtual machines.

After you've added the services, you'll want to price them. Scrolling down on the Pricing Calculator page will show you customizable details for that service that apply to pricing. For example, on virtual machines, you can select details such as the region, operating system, and instance size. These options all impact the pricing for the VM. You'll see a subtotal for the service. Further down the page, you'll see the full total for all services included in the estimate. Along with the total, you'll see buttons where you can export, save, and share the estimate.

#### 4.2 Estimate a solution

From our original scenario, let's imagine that this system will run on two Azure VMs and will connect to an Azure SQL Database instance. We also want to have a layer 7 load balancer in place to ensure we have enhanced load-balancing capabilities. The following illustration shows an application gateway connected to two virtual machines that are connected to a single Azure SQL Database instance.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/2-estimate-costs-architecture.png)

We can use the Azure pricing calculator to figure out what the solution will cost and export our estimate to share with the team. From the **Example Scenarios** tab, you can add all the resources involved with a common solution to the problem you are trying to solve to estimate all the potential costs. You can also add individual products from the **Products** tab to create an estimate for your custom solution.

![](../image/F12_caculator_tip.png)

In the **Products** tab of the Azure pricing calculator, add the following services to the estimate by clicking on them:

-   **Virtual Machines** in the **Compute** category

-   **Azure SQL Database** in the **Databases** category

-   **Application Gateway** in the **Networking** category

We can configure the details of each, on the **Saved Estimates** tab, to get a solid estimate of our costs. Use the West US region for all resources.

-   **Virtual Machines**. This project is an ASP.NET application, so we'll need to use a **Windows** operating system VM. This application doesn't require a massive amount of computing power, so select the **D2 v3** instance size. We'll need two virtual machines, and they will run all the time (730 hours/month). We're going to use **Standard SSD** storage for these VMs and will require just one disk per VM of size **E10**, for a total of two disks. Keep the storage transactions set to the default of 100.

-   **SQL Database**. For the database, we're going to provision a **Single Database** type using the **vCore** model. We want a **General Purpose**, **Gen 5** database with **8 vCores**. We'll need **32 GB** of storage.

-   **Application Gateway**. For Application Gateway, we're going to use the **Web Application Firewall** tier, so we have some protection for our environment. And we're going to go with just **2** instances and **Medium** size, as our load isn't going to be high. We expect to process **1 TB** of data per month. We don't expect to process any data in the North America, Europe (Zone 1).

Looking through your estimate, you should see a summary cost for each service you've added and a full total for the entire estimate. You can try playing with some of the options - particularly the location you place these resources in - to see the estimate go up or down.

![](../image/F12_location_tip.png)

#### 4.3 Share and save your estimate

We now have an estimate for our solution. We can save this estimate, so we can come back to it later and adjust it if necessary. We can also export it to Excel for further analysis or share the estimate via a URL.

To export the estimate, select **Export** at the bottom of the estimate. Exporting will download your estimate in Excel **(.xlsx)** format and will include all the services you added to your estimate.

We can either share the Excel spreadsheet, or we can click on the Share button in the calculator. Sharing will give you a URL that you can use to share this estimate. Anyone with this link will be able to access it, making it easy to share with your team.

If you are logged in with your Azure account, you can save the estimate, so you can come back to it later. Go ahead and click the **Save** button. If you are signed in, you should see a notification that your estimate was saved. If you aren't signed in, you'll see a message to sign in to save your estimate. After you've saved the estimate, scroll back up to the top of the page and select the **Saved Estimates** tab. You will see your estimate there. You can then select it to pull it back up, or delete it if you no longer need it.

We have arrived at a cost estimate for a set of Azure services without spending any money. We didn't create anything, and we have a fully sharable estimate that we can do further analysis or modifications on in the future. You can use this estimate not only to create estimates for systems where you know the specific services you plan to use but also to compare how different services might impact your overall costs. An example is Microsoft SQL Server on a VM instead of an Azure SQL Database.

![](../image/F12_caculator_knowledge_check.png)

### Topic 5: Exercise - Predict and optimize with Cost Management and Azure Advisor

We learned how to estimate costs before you deploy services on Azure, but what if you already have resources deployed? How do you get visibility into the costs you're already accruing? If we had deployed our previous solution to Azure and now want to make sure that we've sized the virtual machines properly and predict how much our bill will be, how can we do this review? Let's look at a few tools on Azure that you can use to help you solve this problem.

#### 5.1 What is Azure Advisor?

**Azure Advisor** is a free service built into Azure that provides recommendations on high availability, security, performance, operational excellence, and cost. Advisor analyzes your deployed services and looks for ways to improve your environment across each of these areas. We'll focus on the cost recommendations, but you'll want to take some time to review the other recommendations as well.

Advisor makes cost recommendations in the following areas:

-   **Reduce costs by eliminating unprovisioned Azure ExpressRoute circuits**. This recommendation identifies ExpressRoute circuits that have been in the provider status of Not Provisioned for more than one month. Advisor recommends deleting the circuit if you aren't planning to provision the circuit with your connectivity provider.

-   **Buy reserved instances to save money over pay-as-you-go**. Advisor will review your virtual machine usage over the last 30 days and determine if you could save money in the future by purchasing reserved instances. Advisor will show you the regions and sizes where you potentially have the most savings and will show you the estimated savings you might achieve from purchasing reserved instances.

-   **Right-size or shutdown underutilized virtual machines**. This analysis monitors your virtual machine usage for 14 days and then identifies underutilized virtual machines. Virtual machines whose average CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered underutilized virtual machines. The average CPU utilization threshold is adjustable up to 20 percent. By identifying these virtual machines, you can decide to resize them to a smaller instance type, reducing your costs.

![](../image/F12_free_account_note.png)

Let's take a look at where you can find Azure Advisor in the portal.

1.  Sign in to the [Azure portal](https://portal.azure.com/) using your Microsoft account.

2.  Expand the left-hand navigation from the top-left menu and click on **All Services**.

3.  Click on the **Management + governance** category and find **Advisor**. You can also type `Advisor` in the services filter box to filter on just that name.

4.  Click on Advisor, and you'll be taken to the Advisor recommendations dashboard where you can see all the recommendations for your subscription. You'll see a box for each category of recommendations.

![](../image/F12_advisor_note.png)

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/3-advisor-recommendations.png)

Clicking on the **Cost** box will take you to detailed recommendations where you can see the recommendations that Advisor has.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/3-advisor-cost-recommendations.png)

Clicking on any recommendation will take you to the details for that specific recommendation. Then you'll be able to take a specific action, such as resizing virtual machines to reduce spending.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/3-advisor-resize-vm.png)

These recommendations are all places where you might be inefficiently spending money. They're a great place to start and continue to revisit when looking for places to reduce costs. In our example, there's an opportunity for us to save around $700 per month if we take these recommendations. This savings adds up, so be sure to review these recommendations periodically across all areas.

#### 5.2 Azure Cost Management

Azure Cost Management is another free, built-in Azure tool that can be used to gain greater insights into where your cloud money is going. You can see historical breakdowns of what services you are spending your money on and how it is tracking against budgets that you have set. You can set budgets, schedule reports, and analyze your cost areas.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/3-cost-management.png)

As you can see, Azure offers tools at no additional cost that you can use to track and predict your cloud spend and identify where your environment may be inefficient from a cost perspective. You'll want to make sure you make it a regular practice to review the reports and recommendations that these tools make available, so you can unlock savings across your cloud footprint.

#### 5.3 Check your knowledge

![](../image/F12_advisor_knowledge_check.png)

### Topic 6: Exercise - Estimate the Total Cost of Ownership with the Azure TCO calculator

The pricing calculator and cost management advisor can help you predict and analyze your spend for new or existing services.

If you are starting to migrate to the cloud, a useful tool you can use to predict your cost savings is the **Total Cost of Ownership** (TCO) calculator. To use the TCO calculator, you need to complete four steps.

#### Step 1: Open the TCO calculator

Start by browsing to the [Total Cost of Ownership calculator](https://azure.microsoft.com/pricing/tco/) website.

#### Step 2: Define your workloads

Start by entering details about your on-premises infrastructure into the TCO calculator according to four groups:

![](../image/F12_define_workload.png)

#### Step 3: Adjust assumptions

Adjust the values of assumptions that the TCO calculator makes, which might vary between customers. To improve the accuracy of the TCO calculator, you should adjust the values so they match the costs of your current on-premises infrastructure. The assumptions you can customize include:

-   Virtual machine costs

-   Electricity costs

-   Storage costs

-   IT labor costs

-   Hardware costs

-   Software costs

-   Virtualization costs

-   Datacenter costs

-   Networking costs

-   Database costs

#### Step 4: View the report

The TCO calculator generates a detailed report based on the details you enter and the adjustments you make. The report allows you to compare the costs of your on-premises infrastructure with the costs of using Azure products and services to host your infrastructure in the cloud.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/3a-tco-calculator-report.png)

### Topic 7: Save on infrastructure costs

We have seen how to create cost estimates for environments you'd like to build, walked through some tools to get details on where we're spending money, and projected future expenses. Our next challenge is to look at how to reduce those infrastructure costs.

#### 7.1 Use Azure credits

Visual Studio subscribers can activate a monthly credit benefit that allows you to experiment with, develop, and test new solutions on Azure. Use Azure credits to try out new services such as App Service, Windows 10 VMs, Azure SQL Server databases, Containers, Cognitive Services, Functions, Data Lake, and more, without incurring any monetary costs.

When you activate this benefit, you will own a separate Azure subscription under your account with a monthly credit balance that renews each month while you remain an active Visual Studio subscriber.

The credit amount varies based on the program level, and you should check the documentation for more details on how much credit you receive for your specific subscription level. For example:

-   $50 per month for Visual Studio Professional

-   $150 per month for Visual Studio Enterprise

![](../image/F12_azure_credit_imp.png)

#### 7.2 Use spending limits

By default, Azure subscriptions that have associated monthly credits (which includes trial accounts) have a spending limit to ensure you aren't charged once you have used up your credits. This feature is useful for development teams exploring new solution architectures as it ensures you won't have an unexpectedly large bill at the end of the month.

![](../image/F12_spend_limit_note.png)

Azure provides the spending limits feature to help prevent you from exhausting the credit on your account within each billing period. When your Azure usage results in charges that use all the included monthly credit, the services that you deployed are disabled and turned off for the rest of that billing period. Once a new billing period starts, assuming there are credits available, the resources are reactivated and deployed.

You are notified by email when you hit the spending limit for your subscription. In addition, the Azure portal includes notifications about your credit spend. You can adjust the spending limit as desired or turn it off completely.

![](../image/F12_spend_limit_imp.png)

#### 7.3 Use reserved instances

If you have virtual machine workloads that are static and predictable, using reserved instances is a fantastic way to potentially save up to 70 to 80 percent off the pay-as-you-go cost. The savings can be significant, depending on the VM size and duration the machine runs. The following illustration shows that using Azure reserved instances saves you up to 72 percent and using reserved instance plus Azure Hybrid Benefit saves up to 80 percent in costs.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/4-savings-coins.png)

You commit to reserved instances in one-year or three-year terms. Payment can be made in full for the entire commitment period, or the commitment can be billed monthly. After it's reserved, Microsoft matches up the reservation to running instances and decrements the hours from your reservation. Reservations can be purchased through the Azure portal. And because reserved instances are a compute discount, they are available for both Windows and Linux VMs.

#### 7.4 Choose low-cost locations and regions

The cost of Azure products, services, and resources can vary across locations and regions, and if possible, you should use them in those locations and regions where they cost less.

![](../image/F12_region_cost_note.png)

#### 7.5 Research available cost-saving offers

Keep up to date with the latest Azure customer and subscription offers, and switch to offers that provide the most significant cost-saving benefit.

You can check the [Azure Updates page](https://azure.microsoft.com/updates/) for information about the latest updates to Azure products, services, and features, as well as product roadmaps and announcements.

#### 7.6 Right-size underutilized virtual machines

Recall from our previous discussion that Azure Cost Management and Azure Advisor might recommend right-sizing or shutting down VMs. Right-sizing a virtual machine is the process of resizing it to a proper size. Let's imagine you have a server running as a domain controller that is sized as a Standard\_D4sv3, but your VM is sitting at 90 percent idle the vast majority of the time. By resizing this VM to a Standard\_D2sv3, you reduce your compute cost by 50 percent. Costs are linear and double for each size larger in the same series. In this case, you might even benefit from changing the instance series to go to a less expensive VM series. The following illustration shows a 50 percent savings achieved by moving one size down within the same series.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/4-vm-resize.png)

Over-sized virtual machines are a common unnecessary expense on Azure, and one that can be easily fixed. You can change the size of a VM through the Azure portal, Azure PowerShell, or the Azure CLI.

![](../image/F12_vm_tip.png)

#### 7.7 Deallocate virtual machines in off hours

If you have virtual machine workloads that are only used during certain periods, but you're running them every hour of every day, you're wasting money. These VMs are great candidates to shut down when not in use and start back up on a schedule, saving you compute costs while the VM is deallocated.

This approach is an excellent strategy for development environments. It's often the case that development may happen only during business hours, giving you the flexibility to deallocate these systems in the off hours and stopping your compute costs from accruing. Azure now has an [automation solution](https://docs.microsoft.com/azure/automation/automation-solution-vm-management) fully available for you to leverage in your environment.

You can also use the **auto-shutdown** feature on a virtual machine to schedule automated shutdowns.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/4-vm-auto-shutdown.png)

#### 7.8 Delete unused virtual machines

This advice may sound obvious, but if you aren't using a service, you should shut it down. It's not uncommon to find non-production or proof-of-concept systems that are no longer needed following the completion of a project. Regularly review your environment and work to identify these systems. Shutting down these systems can have a multifaceted benefit by saving you not only on infrastructure costs but also potential savings on licensing and operations.

#### 7.9 Migrate to PaaS or SaaS services

Lastly, as you move workloads to the cloud, a natural evolution is to start with infrastructure-as-a-service (IaaS) services and then move them to platform-as-a-service (PaaS) services, as appropriate, in an iterative process.

PaaS services typically provide substantial savings in both resource and operational costs. The challenge is that depending on the type of service, **varying levels of effort will be required to move to these services**, from both a time and resource perspective. You might be able to move a SQL Server database to Azure SQL Database easily, but it might take substantially more effort to transfer your multi-tier application to a container or serverless-based architecture. It's a good practice to continuously evaluate the architecture of your applications to determine if there are efficiencies to be gained through PaaS services.

Azure makes it easy to test these services with little risk, giving you the ability to try out new architecture patterns relatively easily. That said, it's typically a longer journey and might not be of immediate help if you're looking for quick wins from a cost-savings perspective. The Azure Architecture Center is a great place to get ideas for transforming your application, as well as best practices across a wide array of architectures and Azure services.

#### 7.10 Check your knowledge

![](../image/F12_infrastructure_knowledge_check.png)

### Topic 8: Save on licensing costs

Licensing is another area that can dramatically impact your cloud spending. Let's look at some ways you can reduce your licensing costs.

#### 8.1 Linux vs. Windows

Many of the Azure services you deploy have the choice of running on Windows or Linux. In some cases, the cost of the product can be different based on the OS you choose. Where you have a choice, and your application doesn't depend on the underlying OS, it's useful to compare pricing to determine whether you can save money.

#### 8.2 Azure Hybrid Benefit for Windows Server

Many customers have invested in Windows Server licenses and would like to repurpose this investment on Azure. The Azure Hybrid Benefit gives customers the right to use these licenses for virtual machines on Azure.

To be eligible for this benefit, your Windows licenses must be covered by Software Assurance. The following guidelines will also apply:

-   Each two-processor license or each set of 16-core licenses is entitled to two instances of up to eight cores or one instance of up to 16 cores.

-   Standard Edition licenses can only be used either on-premises or in Azure, but not both. That means you can't use the same license for an Azure VM and a local computer.

-   Datacenter Edition benefits allow for simultaneous usage both on-premises and in Azure so that the license will cover two running Windows machines.

![](../image/F12_license_note.png)

Applying the benefit is easy. It can be turned on and off at any time with existing VMs or applied at deployment time for new VMs. The Hybrid Benefit can provide substantial license savings, especially when combined with reserved instances.

#### 8.3 Azure Hybrid Benefit for SQL Server

The Azure Hybrid Benefit for SQL Server helps you maximize the value from your current licensing investments and accelerate your migration to the cloud. Azure Hybrid Benefit for SQL Server is an Azure-based benefit that enables you to use your SQL Server licenses with active Software Assurance to pay a reduced rate.

You can use this benefit even if the Azure resource is active, but the reduced rate will only be applied from the time you select it in the portal. No credit will be issued retroactively.

##### 8.3.1 Azure SQL Database vCore-based options

For Azure SQL Database, the Azure Hybrid Benefit works as follows:

-   If you have Standard Edition per-core licenses with active Software Assurance, you can get one vCore in the General Purpose service tier for every one license core you own on-premises.

-   If you have Enterprise Edition per-core licenses with active Software Assurance, you can get one vCore in the Business Critical service tier for every one license core you own on-premises. The Azure Hybrid Benefit for SQL Server for the Business Critical service tier is available only to customers who have Enterprise Edition licenses.

-   If you have highly virtualized Enterprise Edition per-core licenses with active Software Assurance, you can get four vCores in the General Purpose service tier for every one license core you own on-premises. The vCore benefit is a unique virtualization benefit available only on Azure SQL Database.

The following illustration shows the vCore-based options available in each service tier with Azure Hybrid Benefit for SQL Server licenses.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/5-sql-tradein-value.png)

For SQL Server in Azure Virtual Machines, the Azure Hybrid Benefit works as follows:

-   If you have Enterprise Edition per-core licenses with active Software Assurance, you can get one core of SQL Server Enterprise Edition in Azure Virtual Machines for every one license core you own on-premises.

-   If you have Standard Edition per-core licenses with active Software Assurance, you can get one core of SQL Server Standard Edition in Azure Virtual Machines for every one license core you own on-premises.

This license arrangement can make a dramatic impact on your Azure spending with SQL Server workloads.

#### 8.4 Use Dev/Test subscription offers

The [Enterprise Dev/Test](https://azure.microsoft.com/offers/ms-azr-0148p/) and [Pay-As-You-Go (PAYG) Dev/Test](https://azure.microsoft.com/offers/ms-azr-0023p/) offers are a benefit you can take advantage of to save costs on your non-production environments. This benefit gives you several discounts, most notably for Windows workloads, eliminating license charges and only billing you at the Linux rate for virtual machines. SQL Server and other Microsoft software covered under a Visual Studio subscription (formerly known as MSDN) are also included.

There are a few requirements for this benefit. First, it's **only for non-production workloads**. This benefit also requires any users of these environments (excluding testers) **must be covered under a Visual Studio subscription**. In short, for non-production workloads, this benefit allows you to save money on your Windows, SQL Server, and other Microsoft virtual machine workloads.

For full details of each offer, check out the offer links above. If you are a customer on an Enterprise Agreement, you'd want to leverage the Enterprise Dev/Test offer, and if you are a customer without an Enterprise Agreement and are instead using PAYG accounts, you'd leverage the Pay-As-You-Go Dev/Test offer.

#### 8.5 Bring your own SQL Server license

If you are a customer on an Enterprise Agreement and already have an investment in SQL Server licenses, and they have freed up as part of moving resources to Azure, you can provision **bring your own license** (BYOL) images off the Azure Marketplace, giving you the ability to take advantage of these unused licenses and reduce your Azure VM cost. You've always been able to use these licenses by provisioning a Windows VM and manually installing SQL Server, but this process simplifies the creation process by leveraging Microsoft certified images. Search for **BYOL** in the Marketplace to find these images.

![](https://docs.microsoft.com/en-gb/learn/modules/predict-costs-and-optimize-spending/media/5-byol-sql-server.png)

![](../image/F12_byol_imp.png)

#### 8.6 Use SQL Server Developer Edition

Many people are unaware that SQL Server Developer Edition is a free product for **nonproduction use**. Developer Edition has all the same features that Enterprise Edition has, but for nonproduction workloads, you can save dramatically on your licensing costs.

Look for SQL Server images for Developer Edition on the Azure Marketplace and use them for development or testing purposes to eliminate the additional cost for SQL Server in these cases.

![](../image/F12_full_license_tip.png)

#### 8.7 Use constrained instance sizes for database workloads

Many customers have high requirements for memory, storage, or I/O bandwidth. But they also often have low requirements for CPU core counts. Based on this popular request, Microsoft has made available the most popular VM sizes (DS, ES, GS, and MS) in new sizes that constrain the vCPU count to one half or one-quarter of the original VM size, while maintaining the same memory, storage, and I/O bandwidth.

![](../image/F12_vm_workload.png)

Because database products like SQL Server and Oracle are licensed per CPU, customers can reduce licensing cost by up to 75 percent and still maintain the high performance their database requires.

#### 8.8 Check your knowledge

![](../image/F12_liecnse_knowledge_check.png)

### Topic 9: Summary

We've talked through the Azure pricing calculator and how you can use it to estimate your costs on Azure and compare pricing between different service offerings. We looked at savings options, how to export pricing estimates, and at tools that Azure has available to help you keep your cloud spend in check.

-   **Azure Advisor** provides *recommendations* in many areas, including cost.

-   **Azure Cost Management** gives you *reporting and billing information*, so you can gain insights into where you're spending your money.

We then explored best practices to help you save money on both infrastructure and licensing.

#### 9.1 Learn more

To learn more about getting more insights into your Azure costs, visit the following articles:

-   [Azure Architecture Center](https://docs.microsoft.com/azure/architecture)

-   [Cost optimization pillar of the Azure Well-Architected Framework](https://docs.microsoft.com/azure/architecture/framework/cost/overview)

-   [Setting up spending limits in Azure](https://docs.microsoft.com/azure/billing/billing-spending-limit)

-   [Azure budgets](https://docs.microsoft.com/azure/billing/billing-cost-management-budget-scenario)

-   [Explore flexible purchasing options for Azure](https://azure.microsoft.com/pricing/purchase-options/)

-   [Understand terms on your Microsoft Azure invoice](https://docs.microsoft.com/azure/billing/billing-understand-your-invoice)

-   [Bandwidth Pricing Detailss](https://azure.microsoft.com/pricing/details/bandwidth/)

#### 9.2 Check your knowledge

![](../image/F12_cost_knowledge_check.png)
