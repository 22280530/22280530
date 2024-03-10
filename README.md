Import graphviz as gv
Styles={
    'graph':{
        'label':'Network Diagram',
        'fontsize':'14',
        'fontcolor':'white',
        'bgcolor':'#444444',
        'rankdir':'BT',
    },
    'nodes':{
        'fontname':'Times new Roman',
        'shape':'box',
        'fontcolor':'white',
        'color':'#00669',
        'style':'filled',
        'fillcolor':'00669',
        'margin':'0.6',
    },
    'edges':{
        'style':'dashed',
        'color':'red',
        'arrowhead':'open',
        'fontname':'Corier',
        'fontsize':'14',
        'fontcolor':'white',
    },
}
def apply_styles(graph,styles):
    graph.graph_attr.update(
        ('graph'in styles and styles['graph']) or {}
        )
    graph.node_attr.update(
        ('nodes'in styles and styles['nodes']) or {}
        )
    graph.edge_attr.update(
        ('edge'in styles and styles['edge']) or {}
        )
        return graph
def draw_topology(topology_dict,output_filename='img/topology'):
    nodes=set([key[0] for key in topology_dict.keys()+topology_dict.values()])
    gl=gv.Graph(format="svg")
    for node in nodes:
             gl.node(node)
             for key,value in topology_dict.iteritems():
                     head,t_label=key
                     tail,h_label=value
                     gl.edge(head,tail,headlabel=h_label,taillabel=t_label,label=""*12)
                     # headport='nw'tailport='s'
                     gl=apply_styles(gl,styles)
print(gl.source)
filename=gl.render(filename=output_filename)
print"Graph saved in",filename
diag5={('X3','Fa0/1'):('X1','Fa0/1'),
       ('X2','Fa3/0'):('X1','Fa3/0'),
       ('X2','Fa1/0'):('X1','Fa0/1'),
       ('X4','Fa4/0'):('X1','Fa4/0'),
       ('X2','Fa0/0'):('X3','Fa0/0'),
       ('X5','Fa4/0'):('X3','Fa3/0'),
       ('X4','Fa1/0'):('X3','Fa0/0'),
       ('X4','Fa1/0'):('X2','Fa1/0'),
       ('X4','Fa0/1'):('X5','Fa0/1')}
draw_topology(diag5)       
                     
    
