# Mesour ArrayManager

Searches, updates, inserts and deletes on two dimensional array

- [Author](http://mesour.com)
- [Contact](http://mesour.com/contact)

# Example array

```php
$your_array = array(
    array('name' => 'John', 'surname' => 'Doe', 'email' => 'john.doe@test.xx'),
    array('name' => 'John', 'surname' => 'Larson', 'email' => 'peter.larson@test.xx'),
    array('name' => 'Claude', 'surname' => 'Graves', 'email' => 'claude.graves@test.xx'),
    array('name' => 'Stuart', 'surname' => 'Norman', 'email' => 'stuart.norman@test.xx'),
    array('name' => 'Kathy', 'surname' => 'Arnold', 'email' => 'kathy.arnold@test.xx'),
    array('name' => 'Jan', 'surname' => 'Wilson', 'email' => 'jan.wilson@test.xx'),
    array('name' => 'Alberta', 'surname' => 'Erickson', 'email' => 'alberta.erickson@test.xx'),
    array('name' => 'Ada', 'surname' => 'Wells', 'email' => 'ada.wells@test.xx'),
    array('name' => 'Ethel', 'surname' => 'Figueroa', 'email' => 'ethel.figueroa@test.xx'),
    array('name' => 'Ian', 'surname' => 'Goodwin', 'email' => 'ian.goodwin@test.xx'),
);
```

# Select

```php
$manager = new \Mesour\ArrayManager($your_array);

$select = $manager->select();

//set keys sensitive to TRUE (default is FALSE)
\Mesour\ArrayManage\Searcher\Condition::setKeysSensitive();

$select->column('*', 'name')
	->where('name', 'John', \Mesour\ArrayManage\Searcher\Condition::EQUAL, 'or')
	->where('name', 'Max', \Mesour\ArrayManage\Searcher\Condition::EQUAL, 'or')
	->where('email', '.xx', \Mesour\ArrayManage\Searcher\Condition::END_WITH, 'and')
	->limit(10)
	->offset(1)
	->orderBy('name', 'ASC');

print_r($select->fetchAll());

print($select->count());
```

# Update

```php
$manager = new \Mesour\ArrayManager($your_array);

$manager->update(array(
	'name' => 'Matouš'
))
->where('name', 'John', \Mesour\ArrayManage\Searcher\Condition::EQUAL)
	->execute();

print_r($your_array); // updated array
```

# Insert

```php
$manager = new \Mesour\ArrayManager($your_array);

$manager->insert(array(
	'name' => 123
))->execute();

print_r($your_array); // updated array
```

# Delete

```php
$manager = new \Mesour\ArrayManager($your_array);

$manager->delete()
	->where('name', 'John', \Mesour\ArrayManage\Searcher\Condition::EQUAL)
	->execute();

print_r($your_array); // updated array
```

# Test

```php
$manager = new \Mesour\ArrayManager($your_array);

$select = $manager->select();

$select->test();
```