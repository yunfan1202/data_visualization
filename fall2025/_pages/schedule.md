---
layout: schedule
permalink: /fall2025/schedule/
title: Schedule
---

** 确切的内容主题和日程安排可能会根据学生的兴趣和课程讨论进行动态调整 **

{% assign current_module = 0 %}
{% assign skip_classes = 0 %}
{% assign prev_date = 0 %}

{% for item in site.data.lectures_2025 %}
{% if item.date %}
{% assign lecture = item %}
{% assign event_type = "upcoming" %}
{% assign today_date = "now" | date: "%s" | divided_by: 86400 %}
{% assign lecture_date = lecture.date | date: "%s" | divided_by: 86400 %}
{% if today_date > lecture_date %}
    {% assign event_type = "past" %}
{% elsif today_date <= lecture_date and today_date > prev_date %}
    {% assign event_type = "warning" %}
{% endif %}
{% assign prev_date = lecture_date %}

<tr class="{{ event_type }}">
    <th scope="row">{{ lecture.date }}</th>
    {% if lecture.title contains 'lectures' %}
    {% assign skip_classes = skip_classes | plus: 1 %}
    <td colspan="4">{{ lecture.title }}</td>
    {% else %}
    <td>
        {{ lecture.title }} <br/>
            <ul>
               {% for topic in lecture.topics %}
                  <li style="font-size:12px;">
                     {{topic}}
                  </li>
               {% endfor %}
        </ul>
    </td>
    <td>
        <ul>
               {% for reading in lecture.readings %}
                  <li style="font-size:12px;">
                     {{reading}}
                  </li>
               {% endfor %}
        </ul>
    </td>
    {% endif %}
</tr>
{% else %}
{% assign current_module = current_module | plus: 1 %}
{% assign module = item %}
<tr class="info">
    <td colspan="5" align="center"><strong>{{ module.title }}</strong></td>
</tr>
{% endif %}
{% endfor %}
