
# python-jama

This module offers a light-weight wrapper to the `Jama` [api][1] in Python.

It provides programmatic access to many features of Jama including item
manipulation. The Jama api is documented at <http://ws.jamasoftware.com/latest/>

## Basic Usage

In order to use this API you will need to have access to a Jama instance and an
authenticated account.

Create a configuration file `~/.jama` containing the following. Be sure to replace
with your own instalation's details:

    [soap]
    url = http://jama.example.com/contour/ws/v3/soap/ContourSoapService?wsdl
    account = <username>
    password = <password>

Example to use the api to get an item from jama. The Jama Soap API
[documentation for getItem][3] looks like this:

    getItem(WsAuth token, java.lang.Long itemId)

The Python call to `getItem` simply looks like:

    from jama import API
    api = API()
    item = api('getItem', 1234)

Note that the `WsAuth token` is required by all Jama api calls so is handled
by `python-jama`. The `item` returned by a call to `jama.api` is a `Suds`
object. See the [suds documentation][4] for more information.

An example which gets all direct child items of a particular document type:

    example_leaf = Leaf(JAMA_EXAMPLE_NODE_ID, JAMA_EXAMPLE_TYPE)

    example_item_generator = api.create_leaf_generator(
        example_leaf,
        ('name',
         ('event_code', 'code')
        ))

    for item_dict, jamaid in example_item_generator:
        print(item_dict['name'], item_dict['code'])

## Installation

    pip install python-jama

or download the source package from the project page on [github][2] and run

    python setup.py install

## Development

Development is carried out on the [github project page][2], patches and pull requests welcome!

[1]: http://ws.jamasoftware.com/latest/com/jamasoftware/contour/ws/v3/ContourSoapServiceImpl.html
[2]: https://github.com/dynamiccontrols/python-jama/
[3]: http://ws.jamasoftware.com/latest/com/jamasoftware/contour/ws/v3/ContourSoapServiceImpl.html#getItem(com.jamasoftware.contour.ws.v3.WsAuth, java.lang.Long)
[4]: https://fedorahosted.org/suds/wiki/Documentation
