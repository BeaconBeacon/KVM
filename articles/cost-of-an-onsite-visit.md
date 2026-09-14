# What one onsite visit actually costs

*Nobody buys remote access hardware because it is interesting. They buy it the second time they spend a day driving to a machine to press a key. Run your own numbers below: one avoided trip usually pays for the whole thing.*

## The number that matters is not the mileage

Ask what a site visit costs and most people answer with fuel. That is the
smallest line on the list. A visit to a machine an hour away typically burns:

- Two hours of driving, paid, in both directions
- An hour on site, most of it spent finding out what is wrong
- The fuel, tolls and parking
- The rest of that person's day, which is now gone
- The downtime while everyone waits for them to arrive

The last one is usually the largest and the least measured. If the machine
being down stops other people working, or stops orders being taken, the drive
is a rounding error next to it.

For anything that needs a flight and a hotel, you are into four figures before
anyone has touched a keyboard.

## Work it out with your own numbers

Change anything below. Nothing is sent anywhere — the arithmetic runs in your
browser.

```html
<div class="calc">
  <div class="calc-row">
    <label for="rate">Hourly cost of the person going</label>
    <span class="pre">$</span><input id="rate" type="number" value="60">
  </div>
  <div class="calc-row">
    <label for="hours">Hours the trip takes, door to door</label>
    <input id="hours" type="number" value="5">
  </div>
  <div class="calc-row">
    <label for="travel">Travel expenses: fuel, tolls, flights, hotel</label>
    <span class="pre">$</span><input id="travel" type="number" value="40">
  </div>
  <div class="calc-row">
    <label for="down">Cost of an hour of downtime, if any</label>
    <span class="pre">$</span><input id="down" type="number" value="0">
  </div>
  <div class="calc-row">
    <label for="wait">Hours the machine waits before somebody arrives</label>
    <input id="wait" type="number" value="4">
  </div>
  <div class="calc-row">
    <label for="trips">Trips like this per year</label>
    <input id="trips" type="number" value="4">
  </div>
  <div class="calc-row">
    <label for="share">Share of them fixable with a screen and keyboard</label>
    <input id="share" type="number" value="70"><span class="post">%</span>
  </div>
  <div class="calc-row">
    <label for="price">Price of the hardware, per machine</label>
    <span class="pre">$</span><input id="price" type="number" value="250">
  </div>

  <div class="calc-out">
    <div><span id="perTrip">$0</span><small>one visit</small></div>
    <div><span id="perYear">$0</span><small>avoidable, per year</small></div>
    <div class="hero"><span id="payback">—</span>
      <small>pays for itself after</small></div>
  </div>
</div>

<style>
.calc{border:1px solid var(--border);background:var(--bg2);border-radius:10px;
padding:20px 22px;margin:24px 0}
.calc-row{display:flex;align-items:center;gap:10px;margin-bottom:10px;
font-size:15px}
.calc-row label{flex:1;color:var(--muted)}
.calc input{width:92px;background:var(--bg);color:var(--text);
border:1px solid var(--border);border-radius:6px;padding:6px 8px;
font:inherit;font-size:15px;text-align:right}
.calc .pre,.calc .post{color:var(--muted);font-size:14px}
.calc-out{display:flex;gap:14px;flex-wrap:wrap;margin-top:18px;
padding-top:18px;border-top:1px solid var(--border)}
.calc-out div{flex:1;min-width:140px}
.calc-out .hero{border:1px solid var(--amber);border-radius:8px;
padding:10px 14px;margin:-10px -4px}
.calc-out span{display:block;font-size:26px;font-weight:700;color:var(--amber)}
.calc-out small{color:var(--muted);font-size:13px}
</style>

<script>
(function () {
  var ids = ['rate','hours','travel','down','wait','trips','share','price'];
  function val(id) { return parseFloat(document.getElementById(id).value) || 0; }
  function money(n) {
    return '$' + Math.round(n).toLocaleString('en-US');
  }
  function calc() {
    var trip = val('rate') * val('hours') + val('travel')
             + val('down') * val('wait');
    var year = trip * val('trips') * (val('share') / 100);
    document.getElementById('perTrip').textContent = money(trip);
    document.getElementById('perYear').textContent = money(year);
    // 回本按"避免掉几次出差"算,不按月 —— 一年跑一次的人看月份没有意义
    var el = document.getElementById('payback');
    el.textContent = trip > 0
      ? (val('price') / trip < 1
          ? 'the first trip'
          : Math.ceil(val('price') / trip) + ' trips')
      : '—';
  }
  ids.forEach(function (id) {
    document.getElementById(id).addEventListener('input', calc);
  });
  calc();
})();
</script>
```

**The number to look at is the third one.** With the defaults above — someone
on $60 an hour, five hours door to door, and downtime priced at nothing at all
— one trip costs more than the hardware that would have prevented it. It pays
for itself the first time you don't go.

That is the whole business case, and it does not need a spreadsheet. Everything
after the first avoided trip is money you keep, and the device does not stop
working at the end of the year.

It only takes several trips to break even if the machine is close, the person
going is cheap, and nobody is waiting on it. If that describes your machines,
you probably don't need this.

## What you put in instead of the trip

That last line in the calculator is a piece of hardware that stays plugged
into the machine. Ours is called Beacon, and this is the whole of it:

- It takes the machine's HDMI output, so it sees whatever a monitor would see
- It plugs into a USB port and acts as a keyboard and a mouse
- It has its own network cable, so it is still reachable when the machine
  itself is not
- You open the machine in a browser and use it as though you were in front of
  it

Nothing is installed on the machine being controlled. It cannot tell that its
monitor and keyboard are somewhere else, which is why this keeps working in
the BIOS, at a boot menu, at a recovery screen, and after an update that broke
the operating system — the cases that generate the trips.

There is nothing to open on the router either. The device makes an outbound
connection and the browser session is relayed to it, so it works at a site you
do not control and behind CGNAT.

For the trips that still have to happen, you can send somebody a link to that
one machine without giving them an account, and watch the screen while they
are standing in front of it.

Beacon is not on sale yet. It will be somewhere between $200 and $300, one
time, with no subscription — which is the number the calculator is defaulting
to.

## Which trips actually disappear

This is where the honest arithmetic matters, because the answer is not all of
them. Set that percentage by looking at your own history.

| What went wrong | Avoidable remotely? |
|---|---|
| Machine stuck at a boot menu or a recovery screen | Yes |
| Bad update, wrong kernel, service that won't start | Yes |
| Boot order changed, needs a BIOS setting | Yes |
| OS up but the network config is wrong | Yes |
| Someone needs to see the screen to say what it shows | Yes |
| Power supply, RAM, disk or cable has failed | No |
| Machine needs a part, or a new one | No |
| Building lost power | No |

Most teams find the first group is the majority of their trips, because the
serious hardware failures are rare and the small stranded-machine problems are
constant. Everything in the first group is a screen and a keyboard, which is
exactly what Beacon puts in your browser.

Even the trips that still happen get cheaper: you know what is wrong before
you leave, so you bring the right part and go once instead of twice.

## The cost nobody puts in the spreadsheet

Two more things move the number, and both are invisible until you look:

**The trips that never got made.** A machine that is slightly wrong, but not
wrong enough to justify a drive, stays slightly wrong for months. Remote
access at BIOS level makes the fix cost ten minutes, so it happens the same
day.

**Who has to go.** Site visits are usually done by the person who is most
capable of doing something else. That hour of driving is priced at their
salary, not at what the task was worth.

## Common questions

### How much does one onsite IT visit cost on average?

There is no honest single number, because the downtime and the salary of
whoever goes dominate it, and both vary enormously. With no travel expenses,
no downtime cost, and one person for half a day, the floor is usually a few
hundred dollars. Anything involving a flight is four figures.

### Is a remote KVM cheaper than paying for remote hands at a data centre?

If your machines are in a colocation facility, remote hands is usually
billed per incident with a minimum, and you still have to describe what you
want done and hope it is done correctly. A KVM lets you do it yourself
immediately. For machines in offices, shops or homes, there is nobody to call
in the first place.

### Do I need one on every machine?

One per machine, because it physically plugs into that machine's HDMI and
USB. Start with the machines that are furthest away or that have stranded you
before, not with all of them.

### What if a trip becomes necessary anyway?

You still save most of the cost of that trip, because you arrive knowing
what the screen said, which part is dead, and what to bring. The expensive
version of a site visit is the one where somebody drives out, looks, and
drives back for a cable.

---

Originally published at [beacon-kvm.com](https://beacon-kvm.com/blogs/use-cases/cost-of-an-onsite-visit) · [All articles](README.md) · [Build your own on a Raspberry Pi](../README.md)
