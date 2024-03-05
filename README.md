# Mushroom Card
![image](https://github.com/bremor/ha_bins/assets/34525505/fe5b2617-6ab0-4feb-b684-335ee2b69ff0)

```
type: custom:mushroom-entity-card
entity: sensor.bins
name: Bins
icon_type: entity-picture
layout: vertical
tap_action:
  action: none
hold_action:
  action: none
```
# Template Sensor
My bins run a a 4-weekly schedule

Week 0 is Red and Yellow bins.

Week 1 and 3 are Red and Green bins.

Week 2 is Red, Yellow and Purple bins

Icons have been uploaded into /icons in this repo.

```
template:
  - sensor:
      - name: Bins
        state: >
          {% set days = (now().timetuple().tm_yday / 7) | int % 4 %}
          {% if days == 2 %}
          Red, Yellow, Purple
          {% elif days == 0 %}
          Red and Yellow
          {% else %}
          Red and Green
          {% endif %}
        picture: >
          {% set theme = "light" if states("sun.sun") == "above_horizon" else "dark" %}
          {% set days = (now().timetuple().tm_yday / 7) | int % 4 %}
          {% if days == 2 %}
          /local/icons/bins_red_yellow_purple_{{ theme }}.png
          {% elif days == 0 %}
          /local/icons/bins_red_yellow_{{ theme }}.png
          {% else %}
          /local/icons/bins_red_green_{{ theme }}.png
          {% endif %}
