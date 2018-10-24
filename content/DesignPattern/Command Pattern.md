---
title: "Command Pattern"
layout: page
date: 2018-04-17 23:45
---

# 命令模式

老板给小张分配任务，每次都要当着面给小张讲清楚，太累了

于是老板找了纸和笔，每个任务都在纸上写好，让小张到时候照着执行就好，很舒服。

命令模式 : 将**指令的建立**与**指令的执行**分离 

# 别bb 看代码

确定命令的接收者：

```
public class Employee {
    public void doA() {
        System.out.println("I'm doing A");
    }

    public void doB() {
        System.out.println("I'm doing B");
    }

    public void doC() {
        System.out.println("I'm doing C");
    }
}

```

抽象命令：

```
public interface Command {
    void execute();
}

```

命令的具体实现：

```
public class JobACommand implements Command {

    private Employee employee;

    public JobACommand(Employee employee) {
        this.employee = employee;
    }

    @Override
    public void execute() {
        System.out.println("Let's do A");
        employee.doA();
    }
}

public class JobBCommand implements Command {

    private Employee employee;

    public JobBCommand(Employee employee) {
        this.employee = employee;
    }

    @Override
    public void execute() {
        System.out.println("Let's do B and C");
        employee.doB();
        employee.doC();
    }
}
```

确定命令的调用者：

```
public class Boss {
    private List<Command> commandList;

    public void setCommandList(List<Command> commandList) {
        this.commandList = commandList;
    }

    public void action() {
        for (Command command : commandList) {
            command.execute();
        }
    }
}
```

可以分配任务了

```
public class Main {
    public static void main(String[] args) {
        //这是小张
        Employee zhang = new Employee();
        //给小张确认工作内容
        Command jobACommand = new JobACommand(zhang);
        Command jobBCommand = new JobBCommand(zhang);

        //这是老板
        Boss boss = new Boss();
        List<Command> jobList = new ArrayList();
        jobList.add(jobACommand);
        jobList.add(jobBCommand);
        //老板分配了任务
        boss.setCommandList(jobList);

        boss.action();
    }
}
```

```
Let's do A
I'm doing A
Let's do B and C
I'm doing B
I'm doing C
```