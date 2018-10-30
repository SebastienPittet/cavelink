README
======

|Build Status|

About Cave-Link
~~~~~~~~~~~~~~~

Cave-link is a radio device able to transmit data from a cave. You can
add some measurement sensors. The data is consolidated on creator’s
server (database) and displayed through a webpage where the data is dump
to, as `this example shows`_.

If you own a Cavelink, you should ask Felix Ziegler to get your
specific URL, for the sensors you have.

If you know nothing about Cavelink system, the official `website`_ is
the good place to start. Or maybe, you can also begin with `Wikipedia`_.

What is this repository for?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This python module gather the data by parsing the webpage. You will
then be able to display the data on your dashboard or store it to your
own database. I also provide code samples to better explain this -`see
directory ‘samples’`_-.

How do I get set up?
~~~~~~~~~~~~~~~~~~~~

To ensure a proper setup, I recommend the use of virtualenv (but
optionnal).

::

   sudo apt-get update && sudo apt-get install git python-pip --yes
   mkdir your-project
   cd your-project
   virtualenv venv
   source venv/bin/activate
   sudo pip install cavelink

Then you can use the module that way:

>>> import cavelink
>>> webpage="http://www.cavelink.com/cl/da.php?s=142&g=10&w=1&l=10"
>>> nb_rows = 5
>>> slump = Sensor(webpage, nb_rows)
>>> motiers = slump.getJSON(datefmt='human')  # or datefmt='epoch'
>>> motiers_json = json.loads(motiers)
>>> 
>>> for timestamp in motiers_json['measures']:
>>>    print('%s : %s %s' % (key,
>>>                           motiers_json['measures'][timestamp],
>>>                           motiers_json['sensor']['unit']))

You can also fetch additionnal information, also available from the page.
Please note that the following data is provided in JSON object as well.
This is:

>>> print(slump.station)
>>> print(slump.group)
>>> print(slump.number)
>>> print(slump.unit)

Contribution guidelines
~~~~~~~~~~~~~~~~~~~~~~~

Feel free to submit issue or better, some pull requests !

Who do I talk to?
~~~~~~~~~~~~~~~~~

`sebastien at pittet dot org`_

.. _this example shows: http://www.cavelink.com/cl/da.php?s=106&g=1&w=0&l=10
.. _website: http://www.cavelink.com
.. _Wikipedia: https://de.wikipedia.org/wiki/Cave-Link
.. _see directory ‘samples’: https://github.com/SebastienPittet/cavelink/tree/master/samples
.. _sebastien at pittet dot org: https://sebastien.pittet.org

.. |Build Status| image:: https://travis-ci.org/SebastienPittet/cavelink.svg?branch=master
   :target: https://travis-ci.org/SebastienPittet/cavelink