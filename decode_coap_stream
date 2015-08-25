do
    print ("Registered COAP follow")
    local coap_wrapper_proto = Proto("coap_follow", "Follow the COAP stream");
    local udp_dissector_table = DissectorTable.get("udp.port");
    local original_coap_dissector = udp_dissector_table:get_dissector(5683);
    local f_srcport = Field.new("udp.srcport")
    function coap_wrapper_proto.dissector(tvbuffer, pinfo, treeitem)
        original_coap_dissector:call(tvbuffer, pinfo, treeitem)
        local srcport = tostring(f_srcport())
        if(nil == udp_dissector_table:get_dissector(srcport)) then
            print("Adding coap dissector on port :" .. srcport)
            udp_dissector_table:add(srcport, original_coap_dissector)
        end
    end
    udp_dissector_table:add(5683, coap_wrapper_proto)
end
