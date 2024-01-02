## Strategy Order Flow Summary

1. L1 is the initial entry. Once L1 is entered, no more L1 entries are allowed until L1 is closed. If L2-L5 are entered, all must be closed before a new L1 entry.

2. The entry size and price level for L2-L5 are determined by the average price (AVGLine) of the overall position.

3. AVGLine is calculated as the sum of each entry price multiplied by its trade size, divided by the total trade size. This represents the average entry price of the overall position.

4. The entry price for L2-L5 is a distance away from AVGLine, determined by `atrMultiplier_SO` and `SO_factor` inputs. These are defined in the `entry_levels` array.

5. Additional conditions for L2-L5 entries may be implemented beyond the entry level.

6. Each time a new L2-L5 is entered, AVGLine and the entry levels for L2-L5 are recalculated based on the new average price.

7. AVGLine is plotted on the chart and updated after each entry.

8. The target and stop-loss for each L2-L5 are calculated based on the ATR of the timeframe and the `atrMultiplier_TP` and `atrMultiplier_SL` inputs. These are defined in the `SLlines` and `TPlines` arrays.

9. The target and stop-loss are plotted on the chart. They are the same for all positions and are updated based on AVGLine.

10. entries L2-L5 are entered at lower levels to aid previous entries in exiting position for profit as Avg price and TP level get s moved closer to current price action if script is functioning properly target and stop-loss are the same for all positions and are updated based on AVGLine.

