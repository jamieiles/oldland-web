---
title: Keynsham Soc Configuration
layout: default
---

<h1>Keynsham SoC Configuration</h1>

<h2>CPU</h2>
{% assign cpu = site.data.keynsham.cpu %}
<p><strong>Manufacturer:</strong> {{ cpu.manufacturer }}</p>
<p><strong>Model:</strong> {{ cpu.model }}</p>
<p><strong>Clock Speed:</strong> {{ cpu.clock_speed }}</p>

<h2>Instruction Cache</h2>
<p><strong>Ways:</strong> {{ cpu.icache.num_ways }}</p>
<p><strong>Size:</strong> {{ cpu.icache.size }}</p>
<p><strong>Line size:</strong> {{ cpu.icache.line_size }}</p>

<h2>Data Cache</h2>
<p><strong>Ways:</strong> {{ cpu.dcache.num_ways }}</p>
<p><strong>Size:</strong> {{ cpu.dcache.size }}</p>
<p><strong>Line size:</strong> {{ cpu.dcache.line_size }}</p>

<h2>Memory Map</h2>
<table>
<tr><th>Address</th><th>Size</th><th>Name</th></tr>
{% for p in site.data.keynsham.peripherals | sort: "address" %}
  <tr><td>{{ p.address | HexFilter::as_hex }}</td><td>{{ p.size }}</td><td>{{ p.name }}</td></tr>
{% endfor %}
</table>

<h2>Peripheral Register Maps</h2>

{% for p in site.data.keynsham.peripherals | sort: "address" %}
{% if p.regmap != null %}
<h3>{{ p.name }}</h3>
<table>
<tr><th>Offset</th><th>Name</th><th>Fields</th></tr>
	{% for reg in site.data.regmaps[p.regmap] | sort: "offset" %}
	  <tr><td>{{ reg[1].offset | HexFilter::as_hex }}</td><td>{{ reg[0] }}</td>
	  <td>
		<ul>
		{% for field in reg[1].fields | sort: "offset" %}
		<li>[{{ field[1].width | plus : field[1].offset | minus : 1 }}:{{ field[1].offset }}] {{ field[0] }} </li>
		{% endfor %}
		</ul>
	  </td>
	  </tr>
	{% endfor %}
</table>
{% endif %}
{% endfor %}
