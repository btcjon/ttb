Take your Pine Script® debugging to another level with our new log.\*() functions, which display text in the new Pine Logs pane as the script executes. The three new logging functions are:

-   [log.error()](https://www.tradingview.com/pine-script-reference/v5/#fun_log.error) creates messages of type “Error” displayed in red.
-   [log.info()](https://www.tradingview.com/pine-script-reference/v5/#fun_log.info) creates messages of type “Info” displayed in gray.
-   [log.warning()](https://www.tradingview.com/pine-script-reference/v5/#fun_log.warning) creates messages of type “Warning” displayed in orange.

You can view Pine Logs by selecting “Pine Logs…” from the Editor’s “More” menu, or from the “More” menu of a script loaded on your chart if it uses log.\*() functions.

![](https://tvblog-static.tradingview.com/uploads/2023/08/pine-logs-in-pine-script-4.png)

Pine Logs work everywhere: on historical bars, in real time, and in Replay mode. The logging functions can be called from any type of script (indicator, strategy or library) and from anywhere in the script, including local blocks, loops and from inside [request.security()](https://www.tradingview.com/pine-script-reference/v5/#fun_request.security) and similar functions. You can call logging functions in two ways: using only a string argument, or using a formatting string and a list of values in [str.format()](https://www.tradingview.com/pine-script-reference/v5/#fun_str.format) fashion.

Scripts using logs must be personal scripts; privately or publicly published scripts cannot generate logs, even if they contain calls to log.\*() functions.

The following code example uses all three logging functions:

```
//@version=5
indicator("Pine Logs")
if barstate.ishistory
&nbsp;&nbsp;&nbsp;&nbsp;if bar_index % 100 == 0
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log.warning("\nBar index: {0,number,#}", bar_index)
else
&nbsp;&nbsp;&nbsp;&nbsp;// Realtime bar processing.
&nbsp;&nbsp;&nbsp;&nbsp;varip lastTime = timenow
&nbsp;&nbsp;&nbsp;&nbsp;varip updateNo = 0
&nbsp;&nbsp;&nbsp;&nbsp;if barstate.isnew
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;updateNo := 0
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log.error("\nNew bar")
&nbsp;&nbsp;&nbsp;&nbsp;else
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;log.info("\nUpdate no: {0}\nclose: {1}\nSeconds elapsed: {2}", updateNo, close, (timenow - lastTime) / 1000)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;updateNo += 1
&nbsp;&nbsp;&nbsp;&nbsp;lastTime := timenow
plot(timenow)
```

The example displays the bar index on every hundredth historical bar using an orange warning message. In real time, it displays an error message in red for each new bar, and for each real-time update, it creates an information message in gray showing the update number, the [close](https://www.tradingview.com/pine-script-reference/v5/#var_close) price, and the time elapsed since the last chart update.

To see Pine Logs in action:

1.  Save the above code example to a personal script and add it to a chart with an active market.
2.  Open the “Pine Logs” pane using the Editor’s “More” menu or the indicator’s “More” menu on the chart.

![](https://tvblog-static.tradingview.com/uploads/2023/08/pine-logs-in-pine-script-1.png)

A timestamp prefixes each log entry. It is the bar’s opening [time](https://www.tradingview.com/pine-script-reference/v5/#fun_time) for historical bars, and the current time for real-time messages. Newer messages appear at the bottom of the pane. Only the last 10,000 messages will be displayed for historical bars; real-time messages are appended to those.

The top of the pane contains icons allowing you to start/stop the logging, specify a starting date, filter the logs by message type, and search the logs. The search field contains a sub-menu allowing you to match cases, whole words, and use regex.

When you hover over a log message, icons appear that allow you to view the source code that has generated the message or jump to the corresponding chart bar:

![](https://tvblog-static.tradingview.com/uploads/2023/08/pine-logs-in-pine-script-2.png)

When multiple scripts on your chart use logs, each one maintains its own set of messages. You can switch between each script’s logs by using the dropdown at the top of the Pine Logs pane:

![](https://tvblog-static.tradingview.com/uploads/2023/08/pine-logs-in-pine-script-3.gif)

To stay up to date on new Pine Script® features, keep an eye on the User Manual’s [Release notes](https://www.tradingview.com/pine-script-docs/en/v5/Release_notes.html). The [PineCoders](https://www.tradingview.com/u/PineCoders/) account also broadcasts updates from its [Squawk Box](https://t.me/PineCodersSquawkBox) on Telegram, its [Twitter account](https://twitter.com/PineCoders), and from the [Pine Script® Q&A](https://www.tradingview.com/chat/#BfmVowG1TZkKO235) public chat on TradingView.

We hope you find this highly-requested feature as useful as we think it’ll be, and please do keep sending us your [feedback and suggestions](https://www.reddit.com/r/TradingView/) so we can make the platform the best it can be. We build TradingView for you, and we’re always keen to hear your thoughts.

— Team TradingView