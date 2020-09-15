# codeBeamer-rest-client

## Building

Run `gradlew assembleDist` to generate cliebt code and create a distribution.

## Using the client code

```Java

		ApiClient client = new ApiClient();
		client.setUsername(user);
		client.setPassword(password);
		TrackerItemApi tracker = new TrackerItemApi(client);

		TrackerItem item = new TrackerItem();
		item.setName("Hello Swagger");
		item.setDescriptionFormat(DescriptionFormatEnum.WIKI);
		item.setDescription("__Formatted__ Description");

		Integer createdId = tracker.createTrackerItem(trackerId, null, null, null, item).getId();

		//Update specific fields.
		UpdateTrackerItemField update = new UpdateTrackerItemField()
				.addFieldValuesItem(new ChoiceFieldValue()
						.addValuesItem(new ChoiceOptionReference().id(1))
						.fieldId(14))
				.addFieldValuesItem(new TextFieldValue()
						.value("Hello Swagger - UPDATE1")
						.fieldId(3));

		tracker.updateCustomFieldTrackerItem(createdId, Boolean.FALSE, update);

		//Rewrite whole item
		TrackerItem current = tracker.getTrackerItem(createdId, 1, null);
		current.setName("Hello Swagger - UPDATE2");
		current.setSeverities(Arrays.asList(new ChoiceOptionReference().id(2)));
		tracker.updateTrackerItem(current.getId(), null, null, current);

		TrackerItem v1 = current;
		System.out.println(v1.getName() + ": " + v1.getSeverities());

		TrackerItem v2 = tracker.getTrackerItem(createdId, 2, null);
		System.out.println(v2.getName() + ": " + v2.getSeverities());

		TrackerItem v3 = tracker.getTrackerItem(createdId, 3, null);
		System.out.println(v3.getName() + ": " + v3.getSeverities());
```
