---
title: Get started with unit testing
description: Use Visual Studio to define and run unit tests to maintain code health, and to find errors and faults before your customers do.
ms.custom: SEO-VS-2020
ms.date: 12/22/2020
ms.topic: tutorial
helpviewer_keywords:
- unit testing, create unit test plans
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.technology: vs-ide-test
ms.workload:
- multiple
---
# Get started with unit testing

Use Visual Studio to define and run unit tests to maintain code health, ensure code coverage, and find errors and faults before your customers do. Run your unit tests frequently to make sure your code is working properly.

In this article, the code and illustrations use C#, but the concepts and features apply to .NET languages, C++, Python, JavaScript, and TypeScript.

## Create unit tests

This section describes how to create a unit test project.

1. Open the project that you want to test in Visual Studio.

   For the purposes of demonstrating an example unit test, this article tests a simple "Hello World" C# project named **HelloWorldCore**. The sample code for such a project is as follows:

   ```csharp
   namespace HelloWorldCore

      public class Program
      {
         public static void Main()
         {
            Console.WriteLine("Hello World!");
         }
      }
   ```

1. In **Solution Explorer**, select the solution node. Then, from the top menu bar, select **File** > **Add** > **New Project**.

1. In the new project dialog box, find a unit test project template for the test framework you want to use, such as MSTest, and select it.

   Starting in Visual Studio 2017 version 14.8, the .NET languages include built-in templates for NUnit and xUnit. For C++, you will need to select a test framework supported by the language. For Python, see [Set up unit testing in Python code](../python/unit-testing-python-in-visual-studio.md) to set up your test project.

   > [!TIP]
   > For C#, you can create unit test projects from code using a faster method. For more information, see [Create unit test projects and test methods](../test/unit-test-basics.md#create-unit-test-projects-and-test-methods). To use this method with .NET Core or .NET Standard, Visual Studio 2019 is required.

   The following illustration shows an MSTest unit test, which is supported in .NET.

   ::: moniker range=">=vs-2019"

   ![Unit test project template in Visual Studio 2019](media/vs-2019/add-new-test-project.png)

   Click **Next**, choose a name for the test project, and then click **Create**.

   ::: moniker-end

   ::: moniker range="vs-2017"

   ![Unit test project template in Visual Studio 2019](media/mstest-test-project-template.png)

   Choose a name for the test project, such as HelloWorldTests, and then click **OK**.

   ::: moniker-end

   The project is added to your solution.

   ![Unit test project in Solution Explorer](media/vs-2019/solution-explorer.png)

1. In the unit test project, add a reference to the project you want to test by right-clicking on **References** or **Dependencies** and then choosing **Add Reference**.

1. Select the project that contains the code you'll test and click **OK**.

   ![Add project reference in Visual Studio](media/vs-2019/reference-manager.png)

1. Add code to the unit test method.

   For example, you might use the following code by selecting the correct documentation tab that matches your test framework: MSTest, NUnit, or xUnit (supported on .NET only).

   ### [MSTest](#tab/mstest)

   ```csharp
   using Microsoft.VisualStudio.TestTools.UnitTesting;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      [TestClass]
      public class UnitTest1
      {
         private const string Expected = "Hello World!";
         [TestMethod]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

   ### [NUnit](#tab/nunit)

   ```csharp
   using NUnit.Framework;
   using System.IO;
   using System;

   namespace HelloWorldTests
   {
      public class Tests
      {
         private const string Expected = "Hello World!";

         [SetUp]
         public void Setup()
         {
         }
         [Test]
         public void TestMethod1()
         {
            using (var sw = new StringWriter())
            {
               Console.SetOut(sw);
               HelloWorldCore.Program.Main();

               var result = sw.ToString().Trim();
               Assert.AreEqual(Expected, result);
            }
         }
      }
   }
   ```

    ### [xUnit](#tab/xunit)

    ```csharp
    using System;
    using Xunit;
    using System.IO;
    
    namespace HelloWorldTests
    {
        public class UnitTest1
        {
            private const string Expected = "Hello World!";
            [Fact]
            public void Test1()
            {
                using (var sw = new StringWriter())
                {
                    Console.SetOut(sw);
                    HelloWorldCore.Program.Main();
    
                    var result = sw.ToString().Trim();
                    Assert.Equal(Expected, result);
                }
            }
        }
    }
    ```

    ---

## Run unit tests

1. Open [Test Explorer](../test/run-unit-tests-with-test-explorer.md).

   ::: moniker range=">=vs-2019"
   To open Test Explorer, choose **Test** > **Test Explorer** from the top menu bar (or press **Ctrl** + **E**, **T**).
   ::: moniker-end
   ::: moniker range="vs-2017"
   To open Test Explorer, choose **Test** > **Windows** > **Test Explorer** from the top menu bar.
   ::: moniker-end

1. Run your unit tests by clicking **Run All** (or press **Ctrl** + **R**, **V**).

   ![Run unit tests in Test Explorer](media/vs-2019/test-explorer-run-all.png)

   After the tests have completed, a green check mark indicates that a test passed. A red "x" icon indicates that a test failed.

   ![Review unit test results in Test Explorer](media/vs-2019/unit-test-passed.png)

> [!TIP]
> You can use [Test Explorer](../test/run-unit-tests-with-test-explorer.md) to run unit tests from the built-in test framework (MSTest) or from third-party test frameworks. You can group tests into categories, filter the test list, and create, save, and run playlists of tests. You can also debug tests and analyze test performance and code coverage.

## View live unit test results (Visual Studio Enterprise)

If you are using the MSTest, xUnit, or NUnit testing framework in Visual Studio 2017 or later, you can see live results of your unit tests.

> [!NOTE]
> To follow these steps, Visual Studio Enterprise is required.

1. Turn live unit testing from the **Test** menu by choosing **Test** > **Live Unit Testing** > **Start**.

   ::: moniker range="vs-2017"

   ![Turn on live unit testing](media/live-test-results-start.png)

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Start live unit testing in Visual Studio 2019](media/vs-2019/start-live-unit-testing.png)

   ::: moniker-end

1. View the results of the tests within the code editor window as you write and edit code.

   ![View the results of the tests](media/vs-2019/live-unit-testing-results.png)

1. Click a test result indicator to see more information, such as the names of the tests that cover that method.

   ![Choose the test result indicators](media/vs-2019/live-unit-testing-details.png)

For more information about live unit testing, see [Live unit testing](../test/live-unit-testing-intro.md).

## Use a third-party test framework

You can run unit tests in Visual Studio by using third-party test frameworks such as Boost, Google, and NUnit, depending on your programming language. To use a third-party framework:

- Use the **NuGet Package Manager** to install the NuGet package for the framework of your choice.

- (.NET) Starting in Visual Studio 2017 version 14.6, Visual Studio includes pre-configured test project templates for NUnit and xUnit test frameworks. The templates also include the necessary NuGet packages to enable support.

- (C++) In Visual Studio 2017 and later versions, some frameworks like Boost are already included. For more information, see [Write unit tests for C/C++ in Visual Studio](../test/writing-unit-tests-for-c-cpp.md).

To add a unit test project:

1. Open the solution that contains the code you want to test.

2. Right-click on the solution in **Solution Explorer** and choose **Add** > **New Project**.

3. Select a unit test project template.

   In this example, select [NUnit](https://nunit.org/)

   ::: moniker range=">=vs-2019"

   ![NUnit test project template in Visual Studio 2019](media/vs-2019/nunit-test-project-template.png)

   Click **Next**, name the project, and then click **Create**.

   ::: moniker-end

   ::: moniker range="vs-2017"

   Name the project, and then click **OK** to create it.

   ::: moniker-end

   The project template includes NuGet references to NUnit and NUnit3TestAdapter.

   ![NUnit NuGet dependencies in Solution Explorer](media/vs-2019/nunit-nuget-dependencies.png)

4. Add a reference from the test project to the project that contains the code you want to test.

   Right-click on the project in **Solution Explorer**, and then select **Add** > **Reference**. (You can also add a reference from the right-click menu of the **References** or **Dependencies** node.)

5. Add code to your test method.

   ![Add code to your unit test code file](media/vs-2019/unit-test-method.png)

6. Run the test from **Test Explorer** or by right-clicking on the test code and choosing **Run Test(s)** (or **Ctrl** + **R**, **T**).

## Next steps

> [!div class="nextstepaction"]
> [Unit test basics](../test/unit-test-basics.md)

> [!div class="nextstepaction"]
> [Create and run unit tests for managed code](walkthrough-creating-and-running-unit-tests-for-managed-code.md)
