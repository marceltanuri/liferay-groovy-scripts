//this script is useful when some staging publication gets locked

import com.liferay.portal.service.BackgroundTaskLocalServiceUtil;
import com.liferay.portal.model.BackgroundTask;

import java.util.List;

long groupId = 0; //enter your groupId here
int status = 1;

// STATUS_NEW = 0;
// STATUS_IN_PROGRESS = 1;
// STATUS_FAILED = 2;
// STATUS_SUCCESSFUL = 3;
// STATUS_QUEUED = 4;
// STATUS_CANCELLED = 5;


List<BackgroundTask> backgroundTasks = BackgroundTaskLocalServiceUtil.getBackgroundTasks(groupId, status);
for(BackgroundTask task: backgroundTasks){
	if (task.isInProgress())
	BackgroundTaskLocalServiceUtil.deleteBackgroundTask(task.getPrimaryKey());
	
}

