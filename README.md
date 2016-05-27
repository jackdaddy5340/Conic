# Conic

public class Conic {
	private double g;
	private double h;
	private double a;
	private double b;
	private double[] terms=new double[5];
	private double[] xSide=new double[3];
	private double[] ySide=new double[3];
	private boolean isA=true;
	public Conic(double[] term){
		terms=term;
		g=Math.pow((term[2]/term[0])/2, 2);
		h=Math.pow((term[3]/term[1])/2, 2);
		double[] find={Math.sqrt(terms[0]),Math.sqrt(g),(g+h-terms[4])};
		xSide=find;
		double fact=findFactor(xSide);
		if(fact!=0){
			for(int i=0;i<xSide.length;i++){
				xSide[i]=xSide[i]/fact;
			}
		}
		double[] find2={Math.sqrt(terms[1]),Math.sqrt(h),(g+h-terms[4])};
		ySide=find2;
		fact=findFactor(ySide);
		if(fact!=0){
			for(int i=0;i<ySide.length;i++){
				ySide[i]=ySide[i]/fact;
			} 
		}
		double temp1=xSide[2];double temp2=ySide[2];
		if(temp1>=temp2){
			a=temp1;
			b=temp2;
		}
		else{
			a=temp2;
			b=temp1;
			isA=false;
		}
	}
	private double getLargest(){
		double large=terms[0];
		for(double temp: terms)
			if(temp>large)
				large=temp;
		return large;
	}
	private double findFactor(double[] term){
		for(double i=getLargest();i>0;i--){
			boolean gogo=true;
			for( int j=0;j<term.length;j++){
				if(term[j]%i!=0)
					gogo=false;
			}
			if(gogo)
				return i;
		}
		return 0;
	}
	public String toString(){
		String temp=new String();
		if(isA)
			temp="[(("+xSide[0]+"x-"+xSide[1]+")^2)/"+xSide[2]+"] + [(("+ySide[0]+"y-"+ySide[1]+")^2)/"+ySide[2]+"]";
		else
			temp="[(("+ySide[0]+"y-"+ySide[1]+")^2)/"+ySide[2]+"] + [(("+xSide[0]+"x-"+xSide[1]+")^2)/"+xSide[2]+"]";
		return temp;
	}
}
