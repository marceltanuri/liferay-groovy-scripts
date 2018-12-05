//This groovy script lists all pages using a parameterized embedded portlet

import com.liferay.portal.service.LayoutLocalServiceUtil
import com.liferay.portal.model.Layout
import com.liferay.portal.model.LayoutTypePortlet
import com.liferay.portal.model.Portlet
import java.util.List

groupId =  0; //set your groupid here
embedded_portlet_name = ''; //set the desired embeddedPortletId here. eg: '3' for search portlet

int count = 0
while(count<2){
    isPrivatePages = count==0;

    layouts = LayoutLocalServiceUtil.getLayouts(groupId, isPrivatePages);

    if (isPrivatePages) 
        out.println('Private Pages');	
    else
        out.println('Public Pages');

    for (Layout layout : layouts){
        parentPlid = 1;
        treePath = '';
        parent = layout;
        while(parentPlid != 0) {
            parentPlid = parent.getParentPlid();
            if (parentPlid != 0) {
                parent = LayoutLocalServiceUtil.fetchLayout(parentPlid);
                treePath = parent.getName() + ' / ' + treePath;
            }
            
        }

        if (!treePath.isEmpty()) {
            treePath = '[Tree_Path: ' + treePath.substring(0,treePath.length()-3) +  ']';
        }

        if (layout.isSupportsEmbeddedPortlets()) {
            LayoutTypePortlet layoutTypePortlet = (LayoutTypePortlet)layout.getLayoutType();
            List<String> portletIds = layoutTypePortlet.getPortletIds();

            for (Portlet portlet : layoutTypePortlet.getAllPortlets()) {
                if (portlet.getPortletName().equals(embedded_portlet_name)) {
                    out.println('[Portlet_Id: '+portlet.getPortletName()  + '] [Page_Name: ' + layout.getName() + '] ' + treePath +' [Friendly_URL: ' + layout.getFriendlyURL() + ']');
                }
            }
        }
    }
    count++;
}
