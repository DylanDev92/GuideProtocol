# What is it
A coroutine is typically used for tasks that take some time to complete, such as, performing animations, or waiting for a specific event to occur. Instead of blocking the main thread of execution, which can cause performance issues and make your server crash/freeze. You can use the yield statement to specify when the coroutine should pause and when it should resume. For example, you might use a WaitForSeconds yield statement to pause a coroutine for a specific amount of time before continuing.

We use `StartCoroutine()` to start a coroutine, and yield return new `WaitForSeconds(seconds)` to wait

```cs
public class UseCoroutineGuide : IScript
{
    public UseCoroutineGuide()
    {
        CommandHandler.RegisterCommand("UseCoroutineTest", new Action<ShPlayer>(UseCoroutineTest));
    }
    public void UseCoroutineTest(ShPlayer shPlayer)
    {
        shPlayer.StartCoroutine(TestCoroutine(shPlayer));
    }
    public IEnumerator TestCoroutine(ShPlayer player)
    {
        yield return new WaitForSeconds(10f);
        player.svPlayer.SendGameMessage("This message has been sent 10 seconds after");
    }
}
```
# Progress bar

To start a progress bar we use `player.svPlayer.SvProgressBar(0f, 1f / seconds, idProgress)` and for stopping `player.svPlayer.SvProgressStop(idProgress)`

```cs
public IEnumerator TestCoroutine(ShPlayer player)
{
    player.svPlayer.SvProgressBar(0f, 1f / 10, "testcoroutine");
    yield return new WaitForSeconds(10f);
    player.svPlayer.SendGameMessage("This message has been sent 10 seconds after");
    player.svPlayer.SvProgressStop("testcoroutine");
}
```