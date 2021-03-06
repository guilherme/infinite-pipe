# infinite-pipe

Almost every time you run a Linux command you want want to use the output for another command.

The catch is sometimes you don't know what yet. You need to see the output first and think about it.

That's where the infinite pipe comes in.

## Example

Ok, let's say I'm investigating the processes on a machine.

I might run the following:

```
ps -ef
```

Then I look at the output and decide what to do with it.

Let's say I see that there are some interesting docker processes running so I want to look into those.

So I might then run:

```
ps -ef | grep docker
```

Ok cool, now I want the top result:

```
ps -ef | grep docker | head -n 1
```

OK cool, now get me the pid:

```
ps -ef | grep docker | head -n 1 | awk '{print $2}'
```

Cool, now let's investigate that process:

```
ps -ef | grep docker | head -n 1 | awk '{print $2}' | xargs bash -c 'ls -la /proc/$0/fd'
```

I do this stuff all the time, I'm investigating something and don't know where it might lead me.

Infinite pipe let's you pause the stdout chain, think about your next command and continue until you are finished:

Just run:

```
ps -ef | pipe
```

Now you will see your output and be have a prompt where you can either enter in a new command to act on the output to press enter to quit.

Easy!
