---
title: Oldland Instruction Set
layout: default
---

<h1>Oldland Instruction Set</h1>

<a id="top" />
<p>Arithmetic/Bitwise instructions</p>
<ul>
{% for instr in site.data.instructions.instructions %}
{% if instr[1].class == 0 %}
<li class="instrdef"><a href="#{{ instr[0] }}">{{ instr[0] }}</a></li>
{% endif %}
{% endfor %}
</ul>

<p>Call/Branch/Exception instructions</p>
<ul>
{% for instr in site.data.instructions.instructions %}
{% if instr[1].class == 1 %}
<li class="instrdef"><a href="#{{ instr[0] }}">{{ instr[0] }}</a></li>
{% endif %}
{% endfor %}
</ul>

<p>Load/Store instructions</p>
<ul>
{% for instr in site.data.instructions.instructions %}
{% if instr[1].class == 2 %}
<li class="instrdef"><a href="#{{ instr[0] }}">{{ instr[0] }}</a></li>
{% endif %}
{% endfor %}
</ul>

<p>Miscellaneous instructions</p>
<ul>
{% for instr in site.data.instructions.instructions %}
{% if instr[1].class == 3 %}
<li class="instrdef"><a href="#{{ instr[0] }}">{{ instr[0] }}</a></li>
{% endif %}
{% endfor %}
</ul>

{% for instr in site.data.instructions.instructions %}
<h2><a id="{{ instr[0] }}">{{ instr[0] }}</a></h2>
<p><strong>Class: {{ instr[1].class }}, Opcode: {{ instr[1].opcode }}</strong></p>
<h3>Description</h3>
<p><em>{{ instr[1].description | escape }}</em></p>
{% if instr[1].format != empty %}
  <h3>Instruction Operands</h3>
  <ul>
  {% for operand in instr[1].format %}
  {% assign nops = operand | size %}
    {% if nops == 1 %}
      <li>{{ operand }}</li>
      {{ format | escape }}
    {% else %}
      <li>{{ operand[0] }} or {{ operand[1] }}</li>
    {% endif %}
  {% endfor %}
  </ul>
<p><a href="#top">top of page</a></p>
{% endif %}

{% endfor %}
