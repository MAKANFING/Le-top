# Le-top
class Tondeuse {
  val NORTH = "N"
  val EAST = "E"
  val SOUTH = "S"
  val WEST = "O"
  
  val FORWARD = "A"
  val LEFT = "G"
  val RIGHT = "D"
  val directionMapping = Map(	NORTH -> Map(FORWARD->NORTH
										, LEFT -> WEST
										, RIGHT -> EAST)
							,SOUTH -> Map(FORWARD->SOUTH
										, LEFT -> EAST
										, RIGHT -> WEST)
							,EAST -> Map(FORWARD->EAST
										, LEFT -> NORTH
										, RIGHT -> SOUTH)
							,WEST -> Map(FORWARD->WEST
										, LEFT -> SOUTH
										, RIGHT -> NORTH)
                   
  def deplacement(val Pelouse pelouse: string, val Init_pos init_pos: string)={

        X, Y, O = init_pos
        X, Y = int(X), int(Y)

        assert O in ['N', 'S', 'E', 'W'], "Orientation n'est pas validée"
        assert (0 < X < pelouse.limX) && (
            0 < Y < pelouse.limY), "la position n'est pas validé"

        this.limX = pelouse.limX
        this.limY = pelouse.limY
        this.X = X
        this.Y = Y
        this.O = O
        this.pelouse = pelouse
  }
    def __str__(this)={
        return f"{this.X}, {this.Y}, {this.O}"

    def __repr__(this):
        return f"{this.X}, {this.Y}, {this.O}"

    def copy(this):
        return copy.deepcopy(this)

    def can_move(this, deplacement):
        */ La verification du mouvement de la Tondeuse
        */
        assert deplacement in ['G', 'D', 'A'], "Déplacement non valide"
        tond_bis = this.copy()
        tond_bis.move(deplacement)
        return tond_bis.is_legit()

    def is_legit(this):
        return (0 <= this.X <= this.limX) and (0 <= this.Y <= this.limY)

    def move(deplacement):
        */ Mettre en mouvement
        */
        if deplacement == 'G':
            this.O = Tondeuse.orientation[this.O]['G']

        if deplacement == 'D':
            this.O = Tondeuse.orientation[this.O]['D']

        if deplacement == 'A':

            if (this.O == 'N'):
                this.Y = this.Y + 1
            if (this.O == 'S'):
                this.Y = this.Y - 1
            if (this.O == 'E'):
                this.X = this.X + 1
            if (this.O == 'W'):
                this.X = this.X - 1

    def full_move(chemin)={

        for indice, dep in enumerate(chemin):
            if (this.can_move(dep)):
                
                this.move(dep)
           */ Le chemin à parcourir par la Tondeuse */     
def parse_lines(lines)={
    pos_init, chemin = lines[:2]
    pos_init = pos_init.split()

    return pos_init, chemin, lines[2:]


def main():

    */ Pour lire le fichier engagé 
    */

    with open(sys.argv[1]) as input:
        lines = input.read().splitlines()

    num_tondeuse = 0
    
    */ Delimitation de la carte
    */
    lim = lines[0].split()
    lines = lines[1:]

    pelouse = Pelouse(*lim)
    
    */ Le nombre de Tondeuse
    */
    tonds = []

    while(len(lines) > 1):

        num_tondeuse += 1
        pos_init, chemin, lines = parse_lines(lines)

        println(
            f"limite carte = {lim}, position initiale = {pos_init}, chemin = {chemin}, tondeuse n°{num_tondeuse}")

        tond = Tondeuse(pelouse, pos_init)
        tond.full_move(chemin)

        println(f"Tondeuse {num_tondeuse} : {tond.X} { tond.Y} {tond.O}")

        tonds.append(tond)


if __name__ == "__main__":
    main()
}
}
